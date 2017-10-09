---
title: 'Zelfstudie: Azure Active Directory-integratie met iLMS | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en iLMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e11639-6cea-48c9-b008-246cf686e726
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: da0936de23afcd5a4213aa6f699165f9bfa82c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a>Zelfstudie: Azure Active Directory-integratie met iLMS

In deze zelfstudie leert u hoe toointegrate iLMS met Azure Active Directory (Azure AD).

ILMS integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooiLMS toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooiLMS (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met iLMS tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een iLMS eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van iLMS van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-ilms-from-hello-gallery"></a>Het toevoegen van iLMS van Hallo-galerie
tooconfigure hello integratie van iLMS in Azure AD, moet u tooadd iLMS uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd iLMS via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop op Hallo Hallo dialoogvenster bovenaan.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **iLMS**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_search.png)

5. Selecteer in het deelvenster resultaten hello, **iLMS**, klikt u vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met iLMS op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in iLMS is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in iLMS toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in iLMS.

tooconfigure en eenmalige aanmelding Azure AD-test met iLMS, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker iLMS](#creating-an-ilms-test-user)**  -toohave een equivalent van Britta Simon in iLMS die is gekoppeld toohello Azure AD-weergave van haar.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing iLMS configureren.

**Azure AD tooconfigure eenmalige aanmelding met iLMS, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **iLMS** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_samlbase.png)

3. Op Hallo **iLMS domein en de URL's** sectie, voert u Hallo volgende stappen uit als u wilt dat tooconfigure Hallo toepassing in **IDP** modus gestart:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url.png)

    a. In Hallo **id** textbox plakken Hallo **id** waarde u van kopiëren **serviceprovider** sectie van SAML-instellingen in de beheerportal iLMS.

    b. In Hallo **antwoord-URL** textbox plakken Hallo **eindpunt (URL)** waarde u van kopiëren **serviceprovider** sectie van SAML-instellingen in de beheerportal iLMS met de volgende Hallo patroon`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`

    >[!Note]
    >Deze '123456' is een van de Voorbeeldwaarde van id.

4. Controleer **weergeven geavanceerde instellingen voor URL**, indien gewenst tooconfigure Hallo toepassing in **SP** modus gestart:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url1.png)

    In Hallo **aanmeldings-URL** textbox plakken Hallo **eindpunt (URL)** waarde u van kopiëren **serviceprovider** sectie van SAML-instellingen in de beheerportal iLMS als`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`     

5. tooenable JIT-inrichting, verwacht iLMS toepassing hello SAML asserties in een specifieke indeling. Configureer Hallo claims voor deze toepassing te volgen. U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo **gebruikerskenmerken** sectie op de pagina van de toepassing-integratie. Hallo volgende Schermafbeelding toont een voorbeeld voor deze.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/4.png)
    
    Maak **afdeling, regio** en **deling** kenmerken en Hallo-naam van deze kenmerken in iLMS toevoegen. Alle deze kenmerken die hierboven zijn vereist.    

    > [!NOTE] 
    > U hebt tooenable **Un-recognized-gebruikersaccount maken** in iLMS toomap deze kenmerken. Volg de instructies Hallo [hier](http://support.inspiredelearning.com/customer/portal/articles/2204526) tooget een idee op Hallo kenmerken configuratie.

6. In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in Hallo afbeelding hierboven en uitvoeren van Hallo stappen te volgen:
    
    | Naam van kenmerk | De waarde van kenmerk |
    | ---------------| --------------- |    
    | deling | User.Department |
    | Regio | User.state |
    | Afdeling | User.jobtitle |

    a. Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_05.png)
    
    b. In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.
    
    c. Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.
    
    d. Klik op **Ok**

7. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_certificate.png) 

8. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-iLMS-tutorial/tutorial_general_400.png)

9. Aanmelden in een ander browservenster tooyour **iLMS-beheerportal** als beheerder.

10. Klik op **SSO:SAML** onder **instellingen** tooopen SAML-instellingen op het tabblad en Hallo stappen uitvoeren:
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/1.png) 

    a. Vouw Hallo **serviceprovider** sectie en kopieer Hallo **id** en **eindpunt (URL)** waarde.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/2.png) 

    b. Onder **identiteitsprovider** sectie, klikt u op **metagegevens importeren**.
    
    c. Selecteer Hallo **metagegevens** bestand gedownload van Azure-Portal **certificaat voor ondertekening van SAML** sectie.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    d. Als u wilt dat tooenable JIT inrichting toocreate iLMS accounts voor ongedaan maken-gebruikers herkennen, volgt u onderstaande stappen te volgen:
        
       - Controleer **Account maken voor niet-herkende gebruiker**.
       
       ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  Hallo kenmerken toewijzen in Azure AD met Hallo kenmerken in iLMS. Geef in Hallo kenmerkkolom Hallo-kenmerken naam of het Hallo standaardwaarde.

    e. Ga te**bedrijfsregels** tabblad en Hallo stappen uitvoeren: 
        
       ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/5.png)

       - Controleer **Un-recognized regio's maken, afdelingen en afdelingen** toocreate regio's, afdelingen en afdelingen die gelijktijdig Hallo met eenmalige aanmelding niet al bestaan.
        
       - Controleer **Update gebruiker profiel tijdens aanmelden** toospecify of Hallo gebruikersprofiel wordt bijgewerkt met elke eenmalige aanmelding. 
        
       - Als hello **'Update lege waarden voor niet verplichte velden in gebruikersprofiel'** optie is ingeschakeld, optionele profiel velden leeg bij het aanmelden wordt zijn ook voor zorgen dat Hallo iLMS gebruikersprofiel toocontain lege waarden voor deze velden.
        
       - Controleer **fout meldingse-mail verzenden** en Voer Hallo e-mailadres van de gebruiker Hallo waar u tooreceive Hallo fout meldingse-mail.

11. Klik op **opslaan** knop toosave Hallo instellingen.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/save.png)

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
    
### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ilms-tutorial/create_aaduser_01.png) 

2. Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ilms-tutorial/create_aaduser_02.png) 

3. Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ilms-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ilms-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-an-ilms-test-user"></a>Een testgebruiker iLMS maken

Toepassing ondersteunt Just in time gebruikers inrichten en na verificatie gebruikers automatisch in de toepassing hello gemaakt worden. JIT werkt als u hebt geklikt op Hallo **Un-recognized-gebruikersaccount maken** selectievakje tijdens SAML-configuratie-instelling op iLMS-beheerportal.

Als u handmatig een gebruiker toocreate moet, volgt u onderstaande stappen te volgen:

1. Tooyour iLMS bedrijf site aanmelden als beheerder.

2. Klik op **'Gebruiker registreren'** onder **gebruikers** tabblad tooopen **gebruiker registreren** pagina. 
   
   ![Werknemer toevoegen](./media/active-directory-saas-ilms-tutorial/3.png)

3. Op Hallo **'Gebruiker registreren'** pagina, voert u Hallo stappen te volgen.

    ![Werknemer toevoegen](./media/active-directory-saas-ilms-tutorial/create_testuser_add.png)

    a. In Hallo **voornaam** textbox type Hallo voornaam Britta.
   
    b. In Hallo **achternaam** textbox type Hallo achternaam Simon.

    c. In Hallo **E-mail-ID** textbox type Hallo e-mailadres van Britta Simon account.

    d. In Hallo **regio** vervolgkeuzelijst, selecteer Hallo-waarde voor de regio.

    e. In Hallo **deling** vervolgkeuzelijst, selecteer Hallo-waarde voor deling.

    f. In Hallo **afdeling** vervolgkeuzelijst, selecteer Hallo-waarde voor de afdeling.

    g. Klik op **Opslaan**.

    > [!NOTE] 
    > U kunt registratie mail toouser verzenden door te selecteren **registratie E-mail verzenden** selectievakje.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar tooiLMS toegang verlenen.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooiLMS, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **iLMS**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo iLMS-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour iLMS toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_203.png

