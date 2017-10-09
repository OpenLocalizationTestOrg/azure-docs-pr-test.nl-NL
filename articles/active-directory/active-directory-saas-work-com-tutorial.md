---
title: 'Zelfstudie: Azure Active Directory-integratie met Work.com | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Work.com.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: dcdc51c884abd78c945b649de99f942d32373cf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a>Zelfstudie: Azure Active Directory-integratie met Work.com

In deze zelfstudie leert u hoe toointegrate Work.com met Azure Active Directory (Azure AD).

Work.com integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooWork.com toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooWork.com (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Work.com tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Work.com eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Work.com van Hallo galerie toevoegen
2. Configureren en testen eenmalige aanmelding Azure AD

## <a name="add-workcom-from-hello-gallery"></a>Work.com van Hallo galerie toevoegen
tooconfigure hello integratie van Work.com in Azure AD, moet u tooadd Work.com uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Work.com via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak hello, **Work.com**, selecteer **Work.com** Klik vanuit het deelvenster resultaten **toevoegen** knop tooadd Hallo toepassing.

    ![Uit de galerie toevoegen](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD
In deze sectie configureert en test eenmalige aanmelding Azure AD met Work.com op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Work.com is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Work.com toobe tot stand gebracht.

Wijs in Work.com, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Work.com, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maak een testgebruiker Work.com](#create-a-workcom-test-user)**  -toohave een equivalent van Britta Simon in Work.com die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Work.com configureren.

>[!NOTE]
>tooconfigure eenmalige aanmelding, moet u een aangepaste domeinnaam van Work.com toosetup nog. U moet ten minste een domein toodefine naam, uw domeinnaam testen en implementeren van de hele organisatie tooyour.

**Azure AD tooconfigure eenmalige aanmelding met Work.com, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Work.com** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Op basis van SAML eenmalige aanmelding](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_samlbase.png)

3. Op Hallo **Work.com domein en de URL's** sectie, voert u de volgende Hallo:

    ![Sectie Work.com domein en URL 's](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_url.png)

    In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`http://<companyname>.my.salesforce.com`

    > [!NOTE] 
    > Deze waarde is geen echte. Deze waarde bijwerken Hello werkelijke aanmeldings-URL. Neem contact op met [Work.com Client ondersteuningsteam](https://help.salesforce.com/articleView?id=000159855&type=3) tooget deze waarde. 

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Certificaat voor ondertekening van SAML-sectie](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_certificate.png) 

5. Klik op **opslaan** knop.

    ![De knop Opslaan](./media/active-directory-saas-work-com-tutorial/tutorial_general_400.png)

6. Op Hallo **Work.com configuratie** sectie, klikt u op **configureren Work.com** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![De configuratiesectie Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_configure.png) 
7. Aanmelden tooyour Work.com tenant als administrator.

8. Ga te**Setup**.
   
    ![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")

9. Op Hallo navigatiedeelvenster links in Hallo **beheren** sectie, klikt u op **domeinbeheer** tooexpand Hallo bijbehorende sectie en klik vervolgens op **mijn domein** tooopen hello  **Mijn domein** pagina. 
   
    ![Mijn domein](./media/active-directory-saas-work-com-tutorial/ic767825.png "mijn domein")

10. tooverify die uw domein is correct is ingesteld, zorg ervoor dat deze wordt '**stap 4 geïmplementeerd tooUsers**' en bekijk uw '**mijn domeininstellingen**'.
   
    ![Domein geïmplementeerd tooUser](./media/active-directory-saas-work-com-tutorial/ic784377.png "tooUser domein geïmplementeerd")

11. Meld u bij tooyour Work.com tenant.

12. Ga te**Setup**.
    
    ![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")

13. Vouw Hallo **beveiligingsmechanismen** menu en klik vervolgens op **instellingen voor eenmalige aanmelding**.
    
    ![Eenmalige aanmelding instellingen](./media/active-directory-saas-work-com-tutorial/ic794113.png "eenmalige aanmelding-instellingen")

14. Op Hallo **instellingen voor eenmalige aanmelding** dialoogvenster pagina, voert u Hallo stappen te volgen:
    
    ![SAML ingeschakeld](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML ingeschakeld")
    
    a. Selecteer **SAML ingeschakeld**.
    
    b. Klik op **Nieuw**.

15. In Hallo **SAML Single Sign-On-instellingen** sectie, voert u Hallo stappen te volgen:
    
    ![Afzonderlijke SAML aanmelding instelling](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML Single Sign-On-instelling")
    
    a. In Hallo **naam** textbox, typ een naam voor uw configuratie.  
       
    > [!NOTE]
    > Om een waarde voor **naam** Hallo automatisch invullen **API-naam** textbox.
    
    b. In **verlener** textbox plakken Hallo-waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.
    
    c. certificaat van de tooupload Hallo gedownload vanuit Azure-portal klikt u op **Bladeren**.
    
    d. In Hallo **entiteit-Id** textbox type `https://salesforce-work.com`.
    
    e. Als **SAML identiteitstype**, selecteer **Assertion bevat Hallo Federatie-ID van het gebruikersobject Hallo**.
    
    f. Als **SAML identiteit locatie**, selecteer **identiteit is in Hallo NameIdentfier element van Hallo onderwerp instructie**.
    
    g. In **identiteit Provider aanmeldings-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.

    h. In **identiteit Provider afmelding URL** textbox plakken Hallo-waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.
    
    ik. Als **Provider geïnitieerd aanvragen servicebinding**, selecteer **HTTP Post**.
    
    j. Klik op **Opslaan**.

16. Klik in de klassieke portal van Work.com op Hallo navigatiedeelvenster links op **domeinbeheer** tooexpand Hallo bijbehorende sectie en klik vervolgens op **mijn domein** tooopen hello **mijn domein**pagina. 
    
    ![Mijn domein](./media/active-directory-saas-work-com-tutorial/ic794115.png "mijn domein")

17. Op Hallo **mijn domein** pagina in Hallo **aanmelding pagina huisstijl** sectie, klikt u op **bewerken**.
    
    ![Aanmeldingspagina huisstijl](./media/active-directory-saas-work-com-tutorial/ic767826.png "aanmeldingspagina huisstijl")

14. Op Hallo **aanmelding pagina huisstijl** pagina in Hallo **verificatieservice** sectie, Hallo-naam van uw **SAML SSO instellingen** wordt weergegeven. Selecteer deze en klik vervolgens op **opslaan**.
    
    ![Aanmeldingspagina huisstijl](./media/active-directory-saas-work-com-tutorial/ic784366.png "aanmeldingspagina huisstijl")

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-work-com-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Gebruikers en groepen -> alle gebruikers](./media/active-directory-saas-work-com-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Toevoegen](./media/active-directory-saas-work-com-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Dialoogvenster op de gebruikerspagina](./media/active-directory-saas-work-com-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="create-a-workcom-test-user"></a>Een testgebruiker Work.com maken
Voor Azure Active Directory gebruikers toobe kunnen toosign in, moeten ze ingerichte tooWork.com zijn. In geval van Work.com Hallo is inrichting een handmatige taak.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:
1. Meld u op tooyour Work.com bedrijf site als een beheerder.

2. Ga te**Setup**.
   
    ![Setup](./media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")
3. Ga te**gebruikers beheren \> gebruikers**.
   
    ![Gebruikers beheren](./media/active-directory-saas-work-com-tutorial/IC784369.png "gebruikers beheren")

4. Klik op **nieuwe gebruiker**.
   
    ![Alle gebruikers](./media/active-directory-saas-work-com-tutorial/IC794117.png "alle gebruikers")

5. In Hallo sectie gebruiker bewerken, uitvoeren Hallo stappen hebt uitgevoerd, in de kenmerken van een geldig Azure tekstvakken met betrekking tot AD-account u wilt dat tooprovision in Hallo:
   
    ![Gebruiker bewerken](./media/active-directory-saas-work-com-tutorial/ic794118.png "gebruiker bewerken")
   
    a. In Hallo **voornaam** textbox type Hallo **voornaam** van Hallo gebruiker **Britta**.
    
    b. In Hallo **achternaam** textbox type Hallo **achternaam** van Hallo gebruiker **Simon**.
    
    c. In Hallo **Alias** textbox type Hallo **naam** van Hallo gebruiker **BrittaS**.
    
    d. In Hallo **e** textbox type Hallo **e-mailadres** van gebruiker  **Brittasimon@contoso.com** .
    
    e. In Hallo **gebruikersnaam** textbox, typ een naam van gebruiker, zoals  **Brittasimon@contoso.com** .
    
    f. In Hallo **bijnaam** textbox, typ een **bijnaam** van gebruiker **Simon**.
    
    g. Selecteer **rol**, **gebruikerslicentie**, en **profiel**.
    
    h. Klik op **Opslaan**.  
      
    > [!NOTE]
    > Hello Azure AD-accounthouder krijgt een e-mailbericht met inbegrip van een account koppelen tooconfirm Hallo voordat deze geactiveerd wordt.
    > 
    > 

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooWork.com toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooWork.com, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Work.com**.

    ![Work.com in de lijst van app](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Work.com tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Work.com toepassing.
Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_203.png

