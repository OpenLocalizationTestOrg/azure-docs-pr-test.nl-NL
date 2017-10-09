---
title: 'Zelfstudie: Azure Active Directory-integratie met Kronos | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Kronos.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e28d6191-c375-43c6-b2df-22daa88d9939
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 16fd5c203162d10b78f51b00d79017adaf8632c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kronos"></a>Zelfstudie: Azure Active Directory-integratie met Kronos

In deze zelfstudie leert u hoe toointegrate Kronos met Azure Active Directory (Azure AD).

Kronos integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooKronos toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooKronos (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Kronos tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een **Kronos medewerkers centrale** SSO abonnement ingeschakeld

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Kronos van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-kronos-from-hello-gallery"></a>Het toevoegen van Kronos van Hallo-galerie
tooconfigure hello integratie van Kronos in Azure AD, moet u tooadd Kronos uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Kronos via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Kronos**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_search.png)

5. Selecteer in het deelvenster resultaten hello, **Kronos**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Kronos op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Kronos is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Kronos toobe tot stand gebracht.

Wijs in Kronos, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Kronos, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Kronos](#creating-a-kronos-test-user)**  -toohave een equivalent van Britta Simon in Kronos die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Kronos configureren.

**Azure AD tooconfigure eenmalige aanmelding met Kronos, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Kronos** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_samlbase.png)

3. Op Hallo **Kronos domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_url.png)

    a. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.kronos.net/`

    b. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.kronos.net/wfc/navigator/logonWithUID`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Werk deze waarden met Hallo werkelijke id en de antwoord-URL. Neem contact op met [Kronos ondersteuningsteam](https://www.kronos.in/contact/en-in/form) tooget deze waarden.
 
4. Uw toepassing Kronos verwacht Hallo SAML asserties in een specifieke indeling. Werken met [Kronos ondersteuningsteam](https://www.kronos.in/contact/en-in/form) eerste tooidentify Hallo juiste gebruikers-id, die in de toepassing hello is toegewezen. Neem even ook Hallo hulp bij het Hallo-kenmerk, dat hij of zij wil toouse voor deze toewijzing.
 
     Microsoft raadt u Hallo **'NameIdentifier'** kenmerk als gebruikers-id. U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo **'Gebruikerskenmerken'** sectie op de pagina van de toepassing-integratie.
     
     Hallo volgende Schermafbeelding toont een voorbeeld voor deze. Hier wordt de Hallo hebt toegewezen **gebruikers-id (nameid)** met **ExtractMailPrefix()** functie van **user.userprincipalname**. Dit geeft voorvoegsel op Hallo van e-mailadres van Hallo-gebruiker die is Hallo unieke gebruikersnaam. Dit wordt toohello Kronos toepassing in elke geslaagde reactie verzonden. 
     
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_attribute.png)

5. In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster:

    a. Selecteer in de vervolgkeuzelijst Hallo gebruikers-id, **ExtractMailPrefix**.

    b. In Hallo **Mail** vervolgkeuzelijst, selecteer **user.userprincipalname**.

6. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_certificate.png) 

7. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kronos-tutorial/tutorial_general_400.png)

8. tooconfigure eenmalige aanmelding op **Kronos** zijde, moet u toosend Hallo gedownload **Metadata XML** te[Kronos ondersteuningsteam](https://www.kronos.in/contact/en-in/form). 

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kronos-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kronos-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kronos-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kronos-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-kronos-test-user"></a>Een testgebruiker Kronos maken

In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Kronos maken. Kronos toepassing moet alle Hallo gebruikers toobe ingericht in de toepassing hello voordat u eenmalige aanmelding. 

Werken met Hallo [Kronos ondersteuningsteam](https://www.kronos.in/contact/en-in/form) tooprovision deze gebruikers in de toepassing hello. 

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooKronos toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooKronos, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Kronos**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD SSO-configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Kronos-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Kronos toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_203.png

