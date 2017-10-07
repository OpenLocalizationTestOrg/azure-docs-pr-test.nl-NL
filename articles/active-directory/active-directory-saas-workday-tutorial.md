---
title: 'Zelfstudie: Azure Active Directory-integratie met Workday | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en werkdag.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e9da692e-4a65-4231-8ab3-bc9a87b10bca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: aaa41e372e45f464c4540a70fc79c98dbc06d6b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workday"></a>Zelfstudie: Azure Active Directory-integratie met Workday

In deze zelfstudie leert u hoe toointegrate Workday met Azure Active Directory (Azure AD).

Werkdag integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooWorkday toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooWorkday (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Workday tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een werkdag eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Workday van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-workday-from-hello-gallery"></a>Het toevoegen van Workday van Hallo-galerie
tooconfigure hello integratie van Workday in Azure AD, moet u tooadd Workday uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Workday via Hallo gallery Hallo stappen uitvoeren:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Workday**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workday-tutorial/tutorial_workday_search.png)

5. Selecteer in het deelvenster resultaten hello, **Workday**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workday-tutorial/tutorial_workday_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Workday op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Workday is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Workday toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Workday.

tooconfigure en test eenmalige aanmelding Azure AD met behulp van Workday, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Workday](#creating-a-workday-test-user)**  -toohave een equivalent van Britta Simon in Workday die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw Workday-toepassing.

**Azure AD tooconfigure eenmalige aanmelding met werkdag, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Workday** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workday-tutorial/tutorial_workday_samlbase.png)

3. Op Hallo **Workday-domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workday-tutorial/tutorial_workday_url.png)

    a. In Hallo **aanmeldings-URL** textbox Hallo typewaarde als:`https://impl.workday.com/<tenant>/login-saml2.htmld`

    b. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://impl.workday.com/<tenant>/login-saml.htmld`

    > [!NOTE] 
    > Deze waarden zijn niet Hallo echte. Deze waarden bijwerken met Hallo werkelijke aanmeldings-URL en de antwoord-URL. Uw antwoord-URL bijvoorbeeld een subdomein moet hebben: www, wd2, wd3, wd3 impl, wd5, wd5 impl). Met behulp van ongeveer '*http://www.myworkday.com*' werkt, maar '*http://myworkday.com*' niet. Neem contact op met [Workday Client ondersteuningsteam](https://www.workday.com/en-us/partners-services/services/support.html) tooget deze waarden. 
 

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workday-tutorial/tutorial_workday_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workday-tutorial/tutorial_general_400.png)

6. Op Hallo **Workday configuratie** sectie, klikt u op **configureren Workday** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS>
7. In een ander browservenster, meld u aan tooyour Workday bedrijf site als een beheerder.

8. Ga te**Menu \> Workbench**.
   
    ![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")

9. Ga te**beheer**.
   
    ![Beheer account](./media/active-directory-saas-workday-tutorial/IC782924.png "Account beheer")

10. Ga te**Tenant-instellingen bewerken – beveiliging**.
   
    ![Beveiliging voor de Tenant bewerken](./media/active-directory-saas-workday-tutorial/IC782925.png "Tenant beveiliging bewerken")

11. In Hallo **Omleidings-URL's** sectie, voert u Hallo stappen te volgen:
   
    ![Omleidings-URL's](./media/active-directory-saas-workday-tutorial/IC7829581.png "Omleidings-URL's")
   
    a. Klik op **rij toevoegen**.
   
    b. In Hallo **aanmeldings-URL omleiden** textbox en Hallo **Omleidings-URL mobiele** textbox type Hallo **aanmeldings-URL** ingevoerde op Hallo **Workday-domein en URL's** sectie Hallo Azure-portal.
   
    c. In Azure-portal op Hallo Hallo **eenmalige aanmelding configureren** venster, kopie Hallo **Sign-Out URL**, en plak deze in Hallo **Omleidings-URL voor afmelden** textbox.
   
    d.  In **omgeving** textbox typenaam van het Hallo-omgeving.  

    >[!NOTE]
    > Hallo waarde van Hallo omgeving kenmerk is gekoppeld toohello waarde van de tenant-URL Hallo:  
    >-Als de domeinnaam Hallo van Hallo tenant-URL voor Workday op de bijvoorbeeld met impl begint: *https://impl.workday.com/\<tenant\>/login-saml2.htmld*), Hallo **omgeving** kenmerk moet worden ingesteld als tooImplementation.  
    >-Als de domeinnaam Hallo met iets anders begint, moet u toocontact [Workday Client ondersteuningsteam](https://www.workday.com/en-us/partners-services/services/support.html) tooget Hallo overeenkomende **omgeving** waarde.

12. In Hallo **SAML Setup** sectie, voert u Hallo stappen te volgen:
   
    ![Setup van SAML](./media/active-directory-saas-workday-tutorial/IC782926.png "SAML Setup")
   
    a.  Selecteer **SAML-verificatie inschakelen**.
   
    b.  Klik op **rij toevoegen**.

13. In Hallo sectie SAML-id-Providers, uitvoeren Hallo stappen te volgen:
   
    ![SAML-id-Providers](./media/active-directory-saas-workday-tutorial/IC7829271.png "SAML-id-Providers")
   
    a. Typ de providernaam van een in Hallo identiteit providernaam textbox (bijvoorbeeld: *SPInitiatedSSO*).
   
    b. In de Azure-portal op Hallo Hallo **eenmalige aanmelding configureren** venster, kopie Hallo **SAML entiteit-ID** waarde en plak deze in Hallo **verlener** textbox.
   
    c. Selecteer **werkdag geïnitieerd afmelding inschakelen**.
   
    d. In Azure-portal op Hallo Hallo **eenmalige aanmelding configureren** venster, kopie Hallo **Sign-Out URL** waarde en plak deze in Hallo **verzoek-URL voor afmelden** textbox.

    e. Klik op **openbare sleutel identiteitscertificaat-Provider**, en klik vervolgens op **maken**. 

    ![Maak](./media/active-directory-saas-workday-tutorial/IC782928.png "maken")

    f. Klik op **x509 maken openbare sleutel**. 

    ![Maak](./media/active-directory-saas-workday-tutorial/IC782929.png "maken")


14. In Hallo **weergave x509 openbare sleutel** sectie, voert u Hallo stappen te volgen: 
   
    ![De openbare sleutel weergave x509](./media/active-directory-saas-workday-tutorial/IC782930.png "weergave x509 openbare sleutel") 
   
    a. In Hallo **naam** textbox, typ een naam voor uw certificaat (bijvoorbeeld: *Beschermingsmiddel\_SP*).
   
    b. In Hallo **geldig van** textbox type Hallo geldig vanaf kenmerkwaarde van uw certificaat.
   
    c.  In Hallo **geldig tot** textbox Hallo tooattribute geldige typewaarde van uw certificaat.
   
    > [!NOTE]
    > U kunt Hallo geldig ophalen uit de datum en Hallo geldig toodate van certificaat Hallo gedownload door erop te dubbelklikken.  Hallo datums worden vermeld in Hallo **Details** tabblad.
    > 
    >
   
    d.  Open uw base-64 gecodeerde certificaat in Kladblok en kopiëren Hallo inhoud ervan.
   
    e.  In Hallo **certificaat** textbox plakken Hallo inhoud van het Klembord.
   
    f.  Klik op **OK**.

15. Voer Hallo stappen te volgen: 
   
    ![Configuratie van de SSO-](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "SSO-configuratie")
   
    a.  Hallo inschakelen **x509 persoonlijke sleutelpaar**.
   
    b.  In Hallo **Provider-Service-ID** textbox type **http://www.workday.com**.
   
    c.  Selecteer **inschakelen SP geïnitieerd SAML-verificatie**.
   
    d.  In de Azure-portal op Hallo Hallo **eenmalige aanmelding configureren** venster, kopie Hallo **SAML Single Sign-On Service-URL** waarde en plak deze in Hallo **IdP SSO Service URL** textbox.
   
    e. Selecteer **doen Serviceprovider geïnitieerde verificatieaanvraag niet verkleinen**.
   
    f. Als **aanvragen handtekening verificatiemethode**, selecteer **SHA256**. 
   
    ![Handtekening van de verificatiemethode aanvraag](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "verificatiemethode aanvraag handtekening") 
   
    g. Klik op **OK**. 
   
    ![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE>

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
>

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workday-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workday-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workday-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workday-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-workday-test-user"></a>Maken van een werkdag testgebruiker

een testgebruiker ingericht in Workday tooget, moet u toocontact hello [Workday Client ondersteuningsteam](https://www.workday.com/en-us/partners-services/services/support.html).
Hallo [Workday Client ondersteuningsteam](https://www.workday.com/en-us/partners-services/services/support.html) Hallo gebruiker voor u gemaakt.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooWorkday toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooWorkday, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Workday**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workday-tutorial/tutorial_workday_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

Als u uw instellingen voor eenmalige aanmelding tootest wilt, open Hallo Toegangsvenster. Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Gebruikers inrichten configureren](active-directory-saas-workday-inbound-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workday-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workday-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workday-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workday-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workday-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workday-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workday-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workday-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workday-tutorial/tutorial_general_203.png

