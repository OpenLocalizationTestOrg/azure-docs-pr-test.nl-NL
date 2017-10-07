---
title: 'Zelfstudie: Azure Active Directory-integratie met DocuSign | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en DocuSign.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: e4ef40b8f5af20d811d8d806d2bd7e2039c55052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a>Zelfstudie: Azure Active Directory-integratie met DocuSign

In deze zelfstudie leert u hoe toointegrate DocuSign met Azure Active Directory (Azure AD).

DocuSign integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooDocuSign toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooDocuSign (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met DocuSign tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een DocuSign eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van DocuSign van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-docusign-from-hello-gallery"></a>Het toevoegen van DocuSign van Hallo-galerie
tooconfigure hello integratie van DocuSign in Azure AD, moet u tooadd DocuSign uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd DocuSign via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. Klik op **nieuwe toepassing** knop op Hallo Hallo dialoogvenster bovenaan.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **DocuSign**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_search.png)

5. Selecteer in het deelvenster resultaten hello, **DocuSign**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met DocuSign op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in DocuSign is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in DocuSign toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in DocuSign.

tooconfigure en eenmalige aanmelding Azure AD-test met DocuSign, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker DocuSign](#creating-a-docusign-test-user)**  -toohave een equivalent van Britta Simon in DocuSign die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing DocuSign configureren.

**Azure AD tooconfigure eenmalige aanmelding met DocuSign, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **DocuSign** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_samlbase.png)

3. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base 64)** en sla het bestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_certificate.png) 

4. Op Hallo **DocuSign configuratie** sectie van de Azure-portal klikt u op **DocuSign configureren** venster tooopen configureren eenmalige aanmelding. Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_configure.png)

5. In een andere web-browservenster aanmelding tooyour **DocuSign-beheerportal** als beheerder.

6. Klik in het navigatiemenu aan de linkerkant Hallo Hallo op **domeinen**.
   
    ![Eenmalige aanmelding configureren][51]

7. Klik in het rechterdeelvenster Hallo **Claim domein**.
   
    ![Eenmalige aanmelding configureren][52]

8. Op Hallo **claimen van een domein** dialoogvenster in Hallo **domeinnaam** textbox, typt u het domein van uw bedrijf en klik vervolgens op **Claim**. Zorg ervoor dat u Hallo domein verifiëren en Hallo status actief is.
   
    ![Eenmalige aanmelding configureren][53]

9. Klik in het menu aan de linkerkant Hallo **id-Providers**  
   
    ![Eenmalige aanmelding configureren][54]
10. Klik in het rechterdeelvenster hello, **identiteitsprovider toevoegen**. 
   
    ![Eenmalige aanmelding configureren][55]

11. Op Hallo **identiteit Providerinstellingen** pagina, voert u Hallo stappen te volgen:
   
    ![Eenmalige aanmelding configureren][56]

    a. In Hallo **naam** textbox, typ een unieke naam voor uw configuratie. Gebruik geen spaties.

    b. Plakken **SAML entiteit-ID** in Hallo **identiteit Provider verlener** textbox.

    c. Plakken **SAML Single Sign-On Service-URL** in Hallo **identiteit Provider aanmeldings-URL** textbox.

    d. Plakken **Sign-Out URL** in Hallo **identiteit Provider afmelding URL** textbox.

    e. Selecteer **AuthN aanvraag ondertekenen**.

    f. Als **aanvraag verzenden AuthN door**, selecteer **POST**.

    g. Als **afmelding Verzendaanvraag door**, selecteer **ophalen**.

12. In Hallo **toewijzing van aangepast kenmerk** sectie, kies Hallo veld gewenste toomap met Azure AD Claim. In dit voorbeeld Hallo **emailaddress** claim is toegewezen met de Hallo waarde **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**. Het is Hallo standaardnaam claim van Azure AD voor e-mailbericht claim. 
   
    > [!NOTE]
    > Gebruik Hallo juiste **gebruikers-id** toomap Hallo gebruiker van Azure AD tooDocuSign gebruiker toewijzen. Selecteer Hallo juiste veld en Voer Hallo geschikte waarde op basis van de instellingen van uw organisatie.
          
    ![Eenmalige aanmelding configureren][57]

13. In Hallo **Provider identiteitscertificaat** sectie, klikt u op **certificaat toevoegen**, en u hebt gedownload van Azure AD-portal Hallo-certificaat uploaden.   
   
    ![Eenmalige aanmelding configureren][58]

14. Klik op **Opslaan**.

15. In Hallo **identiteitsproviders** sectie, klikt u op **acties**, en klik vervolgens op **eindpunten**.   
   
    ![Eenmalige aanmelding configureren][59]
 
16. In Hallo **SAML 2.0-eindpunten weergeven** sectie op **DocuSign-beheerportal**, Hallo volgende stappen uit te voeren:
   
    ![Eenmalige aanmelding configureren][60]
   
    a. Kopiëren Hallo **URL-Service Provider verlener**, en plak in Hallo **id** textbox op **DocuSign domein en de URL's** sectie van de Azure portal volgende Hallo Hallo patroon: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.
   
    b. Kopiëren Hallo **aanmeldings-URL voor Service Provider**, en plak in Hallo **aanmelding op URL** textbox op **DocuSign domein en de URL's** sectie van de Azure portal volgende Hallo Hallo patroon: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_url.png)
      
    c.  Klik op **sluiten**
    
17. Klik op Hallo Azure-portal, **opslaan**.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-docusign-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-docusign-tutorial/create_aaduser_02.png) 

3. Bovenaan Hallo Hallo dialoogvenster, klikt u op **toevoegen** tooopen hello **gebruiker** dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-docusign-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-docusign-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-docusign-test-user"></a>Een testgebruiker DocuSign maken

Toepassing ondersteunt **Just in time gebruikersaanvragen** en na verificatie gebruikers automatisch in de toepassing hello gemaakt worden.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar tooDocuSign toegang verlenen.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooDocuSign, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **DocuSign**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo DocuSign tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour DocuSign toepassing.
Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Gebruikers inrichten configureren](active-directory-saas-docusign-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_04.png
[51]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_21.png
[52]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_22.png
[53]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_23.png
[54]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_19.png
[55]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_20.png
[56]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_24.png
[57]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_25.png
[58]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_26.png
[59]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_27.png
[60]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_28.png
[61]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_29.png
[100]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_203.png

