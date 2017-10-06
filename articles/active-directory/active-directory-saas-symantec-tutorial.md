---
title: 'Zelfstudie: Azure Active Directory-integratie met Symantec Web Security Service (WSS) | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Symantec Web Security Service (WSS).
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 9f02b3d4ce2073110c55af4b567b0e3b5a88404f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a>Zelfstudie: Azure Active Directory-integratie met Symantec Web Security Service (WSS)

In deze zelfstudie leert u hoe toointegrate uw Symantec Web Security Service (WSS) rekening met uw account voor Azure Active Directory (Azure AD) zodat WSS een eindgebruiker ingericht in Azure AD Hallo kan verifiëren met behulp van SAML-verificatie en afdwingen van de gebruiker of groep niveau beleidsregels.

Symantec Web Security Service (WSS) integreren met Azure AD biedt Hallo volgende voordelen:

- Alle Hallo end gebruikers en groepen die worden gebruikt door uw WSS-account van uw Azure AD-portal beheren. 

- Hallo end gebruikers tooauthenticate zelf in toestaan WSS met hun Azure AD-referenties.

- Inschakelen Hallo afdwinging van gebruiker en groep niveau beleidsregels die zijn gedefinieerd in uw WSS-account.

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

tooconfigure Azure AD-integratie met Symantec Web Security Service (WSS), moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een account Symantec Web Security Service (WSS)

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met een WSS-account dat momenteel wordt gebruikt voor productie-doel.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw WSS-account dat momenteel wordt gebruikt voor productie-doel voor deze test als dat nodig is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie configureert u uw Azure AD tooenable eenmalige aanmelding tooWSS met de referenties van de eindgebruiker Hallo gedefinieerd in uw Azure AD-account.
Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Hallo Symantec Web Security Service (WSS) app uit de galerie Hallo toevoegen
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-symantec-web-security-service-wss-from-hello-gallery"></a>Het toevoegen van Symantec Web Security Service (WSS) van Hallo-galerie
tooconfigure hello integratie van Symantec Web Security Service (WSS) in Azure AD, moet u tooadd Symantec Web Security Service (WSS) uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Symantec Web Security Service (WSS) uit de galerie hello, Voer Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Hello Azure Active Directory-knop][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Hallo Enterprise toepassingen blade][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![knop voor nieuwe toepassing Hello][3]

4. Typ in het zoekvak Hallo **Symantec Web Security Service (WSS)**, selecteer **Symantec Web Security Service (WSS)** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo de toepassing.

    ![Symantec Web Security Service (WSS) in de lijst met resultaten Hallo](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD

In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Symantec Web Security Service (WSS) hebt op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Symantec Web Security Service (WSS) is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante Hallo-gebruiker in Symantec Web Security Service (WSS) toobe tot stand gebracht.

In Symantec Web Security Service (WSS), wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en test eenmalige aanmelding Azure AD met Symantec Web Security Service (WSS), moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maak een testgebruiker Symantec Web Security Service (WSS)](#create-a-symantec-web-security-service-wss-test-user)**  -toohave een equivalent van Britta Simon in Symantec Web Security Service (WSS) die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Symantec Web Security Service (WSS).

**tooconfigure eenmalige aanmelding Azure AD met Symantec Web Security Service (WSS), Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Symantec Web Security Service (WSS)** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. Op Hallo **Symantec Web Service (WSS) beveiligingsdomein en URL's** sectie, voert u Hallo stappen te volgen:

    ![Symantec Web Security Service (WSS)-domein en de URL's van eenmalige aanmelding informatie](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    a. In Hallo **id** textbox type Hallo URL:`https://saml.threatpulse.net:8443/saml/saml_realm`

    b. In Hallo **antwoord-URL** textbox type Hallo URL:`https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`

    > [!NOTE]
    > Neem contact op met de Hallo [Symantec Web Security Service (WSS) Client ondersteuningsteam](https://www.symantec.com/contact-us) als Hallo voor Hallo waarden **id** en **antwoord-URL** zijn voor een bepaalde reden niet werkt.

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-symantec-tutorial/tutorial_general_400.png)
    
6. Raadpleeg toohello WSS onlinedocumentatie tooconfigure eenmalige aanmelding op Hallo kant Symantec Web Security Service (WSS). Hallo gedownload **Metadata XML** bestand moet toobe geïmporteerd in Hallo WSS-portal. Neem contact op met Hallo [Symantec Web Security Service (WSS) ondersteuningsteam](https://www.symantec.com/contact-us) als u hulp nodig hebt bij Hallo-configuratie op Hallo WSS-portal.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

   ![Een Azure AD-testgebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-symantec-tutorial/create_aaduser_01.png)

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-symantec-tutorial/create_aaduser_02.png)

3. tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.

    ![knop voor Hallo toevoegen](./media/active-directory-saas-symantec-tutorial/create_aaduser_03.png)

4. In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-symantec-tutorial/create_aaduser_04.png)

    a. In Hallo **naam** in het vak **BrittaSimon**.

    b. In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.

    c. Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.

    d. Klik op **Create**.
 
### <a name="create-a-symantec-web-security-service-wss-test-user"></a>Maak een testgebruiker Symantec Web Security Service (WSS)

In deze sectie maakt u een gebruiker met de naam Britta Simon in Symantec Web Security Service (WSS). Hallo overeenkomende end gebruikersnaam kan handmatig worden gemaakt in Hallo WSS-portal of u kunt wachten op Hallo gebruikers/groepen ingericht in hello Azure AD gesynchroniseerd toobe toohello WSS-portal na een paar minuten (~ 15 minuten). Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken. Hallo openbaar IP-adres van de machine eindgebruiker hello, die wordt gebruikt toobrowse websites moet ook toobe ingericht in Hallo Symantec Web Security Service (WSS)-portal.

> [!NOTE]
> Neem [Klik hier](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget uw machine het openbare IP-adres.

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooSymantec Web Security Service (WSS).

![Hallo-gebruikersrollen toewijzen][200] 

**tooassign Britta Simon tooSymantec Web Security Service (WSS) uitvoeren Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Symantec Web Security Service (WSS)**.

    ![Hallo Symantec Web Security Service (WSS) koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_app.png)  

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie maakt u test Hallo één functionaliteit van eenmalige aanmelding nu dat u hebt uw account WSS toouse geconfigureerd uw Azure AD voor SAML-verificatie.

Nadat u hebt geconfigureerd omgeleid uw browser tooproxy webverkeer tooWSS, wanneer u uw webbrowser Open en u vervolgens toobrowse tooa site probeert, moet de pagina toohello Azure eenmalige aanmelding. Hallo referenties opgeven van eindgebruiker van het Hallo-test die is ingericht in hello Azure AD (dat wil zeggen, BrittaSimon) en bijbehorende wachtwoord. Eenmaal is geverifieerd, zult u kunnen toobrowse toohello website die u hebt gekozen. U moet een beleidsregel op Hallo WSS side tooblock BrittaSimon van tooa bepaalde site te bladeren en vervolgens u Hallo WSS blok pagina ziet wanneer u toobrowse toothat site als gebruiker BrittaSimon probeert maken.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_203.png

