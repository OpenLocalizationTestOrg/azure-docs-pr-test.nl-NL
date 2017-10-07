---
title: 'Zelfstudie: Azure Active Directory-integratie met AirWatch | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en AirWatch.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 96a3bb1c-96c6-40dc-8ea0-060b0c2a62e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: e5230d5a36824778a4d9804dadf9f13a0d11a68d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-airwatch"></a>Zelfstudie: Azure Active Directory-integratie met AirWatch

In deze zelfstudie leert u hoe toointegrate AirWatch met Azure Active Directory (Azure AD).

AirWatch integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooAirWatch toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooAirWatch (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met AirWatch tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een AirWatch eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van AirWatch van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-airwatch-from-hello-gallery"></a>Het toevoegen van AirWatch van Hallo-galerie
tooconfigure hello integratie van AirWatch in Azure AD, moet u tooadd AirWatch uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd AirWatch via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **AirWatch**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_search.png)

5. Selecteer in het deelvenster resultaten hello, **AirWatch**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met AirWatch op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in AirWatch is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in AirWatch toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in AirWatch.

tooconfigure en eenmalige aanmelding Azure AD-test met AirWatch, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker AirWatch](#creating-a-airwatch-test-user)**  -toohave een equivalent van Britta Simon in AirWatch die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing AirWatch configureren.

**Azure AD tooconfigure eenmalige aanmelding met AirWatch, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **AirWatch** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_samlbase.png)

3. Op Hallo **AirWatch domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`

    b. In Hallo **id** textbox Hallo typewaarde als`AirWatch`

    > [!NOTE] 
    > Deze waarde is geen echte Hallo. Deze waarde bijwerken met Hallo werkelijke aanmeldings-URL. Neem contact op met [AirWatch Client ondersteuningsteam](http://www.air-watch.com/company/contact-us/) tooget deze waarde. 
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_certificate.png) 

5. Op Hallo **AirWatch configuratie** sectie, klikt u op **configureren AirWatch** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_configure.png) 

6. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS>
7. In een ander browservenster, meld u aan tooyour AirWatch bedrijf site als een beheerder.

8. Klik in het Hallo navigatiedeelvenster links op **Accounts**, en klik vervolgens op **beheerders**.
   
   ![Beheerders](./media/active-directory-saas-airwatch-tutorial/ic791920.png "beheerders")

9. Vouw Hallo **instellingen** menu en klik vervolgens op **Directory Services**.
   
   ![Instellingen](./media/active-directory-saas-airwatch-tutorial/ic791921.png "instellingen")

10. Klik op Hallo **gebruiker** tabblad in Hallo **Base DN** textbox, typ de naam van uw domein en klik vervolgens op **opslaan**.
   
   ![Gebruiker](./media/active-directory-saas-airwatch-tutorial/ic791922.png "gebruiker")

11. Klik op Hallo **Server** tabblad.
   
   ![Server](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Server")

12. Voer Hallo stappen te volgen:
    
    ![Uploaden](./media/active-directory-saas-airwatch-tutorial/ic791924.png "uploaden")   
    
    a. Als **maptype**, selecteer **geen**.

    b. Selecteer **SAML gebruiken voor verificatie**.

    c. tooupload Hallo gedownloade certificaat, klik op **uploaden**.

13. In Hallo **aanvragen** sectie, voert u Hallo stappen te volgen:
    
    ![Aanvraag](./media/active-directory-saas-airwatch-tutorial/ic791925.png "aanvragen")  

    a. Als **Binding aanvraagtype**, selecteer **POST**.

    b. In de Azure-portal op Hallo Hallo **op Airwatch eenmalige aanmelding configureren** dialoogvenster pagina, kopie Hallo **SAML Single Sign-On Service-URL** waarde en plak deze in Hallo **id-Provider Eenmalige aanmelding op URL** textbox.

    c. Als **NameID indeling**, selecteer **e-mailadres**.

    d. Klik op **Opslaan**.

14. Klik op Hallo **gebruiker** tabblad opnieuw.
    
    ![Gebruiker](./media/active-directory-saas-airwatch-tutorial/ic791926.png "gebruiker")

15. In Hallo **kenmerk** sectie, voert u Hallo stappen te volgen:
    
    ![Kenmerk](./media/active-directory-saas-airwatch-tutorial/ic791927.png "kenmerk")

    a. In Hallo **Object-id** textbox type **http://schemas.microsoft.com/identity/claims/objectidentifier**.

    b. In Hallo **gebruikersnaam** textbox type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.

    c. In Hallo **weergavenaam** textbox type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.

    d. In Hallo **voornaam** textbox type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.

    e. In Hallo **achternaam** textbox type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.

    f. In Hallo **e** textbox type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.

    g. Klik op **Opslaan**.

<CE>

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-airwatch-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-airwatch-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-airwatch-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-airwatch-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van Britta Simon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-airwatch-test-user"></a>Een testgebruiker AirWatch maken

Azure AD tooenable gebruikers toolog in tooAirWatch, ze in tooAirWatch moeten worden ingericht.

* AirWatch, inrichting wanneer een handmatige taak is.

**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**

1. Meld u bij tooyour **AirWatch** bedrijf site als administrator.
2. Klik in het navigatievenster aan de linkerkant Hallo Hallo op **Accounts**, en klik vervolgens op **gebruikers**.
   
   ![Gebruikers](./media/active-directory-saas-airwatch-tutorial/ic791929.png "gebruikers")
3. In Hallo **gebruikers** menu, klikt u op **lijstweergave**, en klik vervolgens op **toevoegen \> gebruiker toevoegen**.
   
   ![Gebruiker toevoegen](./media/active-directory-saas-airwatch-tutorial/ic791930.png "gebruiker toevoegen")
4. Op Hallo **toevoegen / bewerken van de gebruiker** dialoogvenster Hallo volgende stappen uit te voeren:

   ![Gebruiker toevoegen](./media/active-directory-saas-airwatch-tutorial/ic791931.png "gebruiker toevoegen")   
   1. Type Hallo **gebruikersnaam**, **wachtwoord**, **wachtwoord bevestigen**, **voornaam**, **achternaam**,  **E-mailadres** van een geldig Azure Active Directory-account die u wilt dat tooprovision in Hallo tekstvakken gerelateerd.
   2. Klik op **Opslaan**.

>[!NOTE]
>U kunt andere AirWatch gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door AirWatch tooprovision AAD-gebruikersaccounts.
>  

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooAirWatch toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooAirWatch, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **AirWatch**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u uw instellingen voor eenmalige aanmelding tootest wilt, open Hallo Toegangsvenster. Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).


## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_203.png

