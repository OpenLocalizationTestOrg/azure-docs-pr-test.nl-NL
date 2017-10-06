---
title: 'Zelfstudie: Azure Active Directory-integratie met T & E Express | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en T & E Express.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: B42374E5-2559-4309-8EF2-820BEE7EBB0C
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: jeedes
ms.openlocfilehash: 9a568ace8dbc75fadbf37554996b1b597a813d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-te-express"></a>Zelfstudie: Azure Active Directory-integratie met T & E Express

In deze zelfstudie leert u hoe toointegrate d & E Express met Azure Active Directory (Azure AD).

D & E Express integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooT heeft & E Express
- U kunt uw gebruikers tooautomatically get aangemelde tooT & E Express (Single Sign-On) inschakelen met hun Azure AD-accounts
- U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met T & E Express tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een d & E Express eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. D & E Express uit Hallo galerie toevoegen
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-te-express-from-hello-gallery"></a>D & E Express uit Hallo galerie toevoegen
tooconfigure hello integratie van d & E Express in Azure AD, moet u tooadd T & E Express uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd T & E Express uit de galerie hello, voert Hallo stappen te volgen:**

1. In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **d & E Express**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_search.png)

5. Selecteer in het deelvenster resultaten hello, **d & E Express**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met T & E Express op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in de T & E Express is tooa gebruiker in Azure AD. Met andere woorden, een relatie koppeling tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in d & E Express behoeften toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in d & E Express.

tooconfigure en test eenmalige aanmelding Azure AD met behulp van d & E Express, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker d & E Express](#creating-a-te-express-test-user)**  -toohave een equivalent van Britta Simon in d & E Express die is gekoppeld toohello Azure AD-weergave van haar.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding configureren in uw toepassing d & E Express.

**tooconfigure eenmalige aanmelding Azure AD met T & E Express, Voer Hallo stappen te volgen:**

1. In hello Azure Management portal op Hallo **d & E Express** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_samlbase.png)

3. Op Hallo **T & E Express domein en URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_url.png)

    a. In Hallo **id** textbox Hallo typewaarde als:`https://<domain>.tyeexpress.com`

    b. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`

    > [!NOTE] 
    > Houd er rekening mee dat deze niet Hallo echte waarden zijn. U hebt deze waarden door de werkelijke id en de antwoord-URL Hallo tooupdate. We raden hier u toouse Hallo unieke waarde van een tekenreeks in Hallo id. Neem contact op met [d & E Express ondersteuningsteam](http://www.tyeexpress.com/contacto.aspx) tooget deze waarden.

5. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_certificate.png) 

6. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_400.png)

8. tooconfigure eenmalige aanmelding op **d & E snelle** aan clientzijde, aanmelding toohello T & E snelle toepassing zonder SAML eenmalige over het gebruik van beheerdersreferenties.

9. Onder Hallo **Admin** tabblad, klikt u op **SAML domein** tooOpen Hallo SAML instellingenpagina.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tyeexpress-tutorial/tye-SAML.png)

10. Selecteer Hallo **Activar(Activate)** optie van **Nee** te**SI(Yes)**. In Hallo **identiteit Provider metagegevens** textbox plakken Hallo metagegevens XML, die u hebt donwloaded vanuit Azure-portal.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tyeexpress-tutorial/tyeAdmin.png)

11. Klik op Hallo **Guardar(Save)** knop toosave Hallo instellingen. 


### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_01.png) 

2. Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_02.png) 

3. Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-te-express-test-user"></a>Maken van een testgebruiker d & E Express

In volgorde tooenable Azure AD gebruikers toolog in d & E Express, moeten ze worden ingericht in d & E Express.  
In geval van een T & E Express is inrichting een handmatige taak.

**tooprovision een gebruikersaccounts uitvoeren Hallo volgende stappen:**

1. Meld u in de tooyour T & E Express bedrijf site als beheerder.

2. Klik op gebruikers tooopen Hallo gebruikers basispagina onder Admin-tag.

    ![Werknemer toevoegen](./media/active-directory-saas-tyeexpress-tutorial/tye-adminusers.png)

3. Klik op de startpagina van Hallo op  **+**  tooadd Hallo gebruikers.

    ![Werknemer toevoegen](./media/active-directory-saas-tyeexpress-tutorial/tye-usershome.png)

4. Alle verplichte Hallo-details in Hallo vorm gevraagd en klik op Hallo opslaan knop toosave Hallo details.

    ![Werknemer toevoegen](./media/active-directory-saas-tyeexpress-tutorial/tye-usersadd.png)

    ![Werknemer toevoegen](./media/active-directory-saas-tyeexpress-tutorial/tye-userssave.png)


### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar toegang tooT & E Express verlenen.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooT & E Express, voert Hallo stappen te volgen:**

1. Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **d & E Express**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u klikt op Hallo T & E Express-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour T & E Express-toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_203.png

