---
title: 'Zelfstudie: Azure Active Directory-integratie met Jobscience | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Jobscience.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 4a4c78aad6d324795a15a9569542afc23b4716d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a>Zelfstudie: Azure Active Directory-integratie met Jobscience

In deze zelfstudie leert u hoe toointegrate Jobscience met Azure Active Directory (Azure AD).

Jobscience integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooJobscience toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooJobscience (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Jobscience tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Jobscience eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Jobscience van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-jobscience-from-hello-gallery"></a>Het toevoegen van Jobscience van Hallo-galerie
tooconfigure hello integratie van Jobscience in Azure AD, moet u tooadd Jobscience uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Jobscience via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Jobscience**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_search.png)

5. Selecteer in het deelvenster resultaten hello, **Jobscience**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Jobscience op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Jobscience is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Jobscience toobe tot stand gebracht.

Wijs in Jobscience, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Jobscience, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Jobscience](#creating-a-jobscience-test-user)**  -toohave een equivalent van Britta Simon in Jobscience die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Jobscience configureren.

**Azure AD tooconfigure eenmalige aanmelding met Jobscience, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Jobscience** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_samlbase.png)

3. Op Hallo **Jobscience domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_url.png)

    In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`http://<company name>.my.salesforce.com`
    
    > [!NOTE] 
    > Deze waarde is geen echte. Deze waarde bijwerken Hello werkelijke aanmeldings-URL. Deze waarde krijgen door [Jobscience Client ondersteuningsteam](https://www.jobscience.com/support) of van Hallo sso-profiel maakt u die later in Hallo zelfstudie wordt uitgelegd. 
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobscience-tutorial/tutorial_general_400.png)

6. Op Hallo **Jobscience configuratie** sectie, klikt u op **configureren Jobscience** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_configure.png) 

7. Aanmelden tooyour Jobscience bedrijf site als beheerder.

8. Ga te**Setup**.
   
   ![Setup](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Setup")

9. Op Hallo navigatiedeelvenster links in Hallo **beheren** sectie, klikt u op **domeinbeheer** tooexpand Hallo bijbehorende sectie en klik vervolgens op **mijn domein** tooopen hello  **Mijn domein** pagina. 
   
   ![Mijn domein](./media/active-directory-saas-jobscience-tutorial/ic767825.png "mijn domein")

10. tooverify die uw domein is correct is ingesteld, zorg ervoor dat deze wordt '**stap 4 geïmplementeerd tooUsers**' en bekijk uw '**mijn domeininstellingen**'.

    ![Domein geïmplementeerd tooUser](./media/active-directory-saas-jobscience-tutorial/ic784377.png "tooUser domein geïmplementeerd")

11. Klik op Hallo Jobscience bedrijf site **beveiligingsmechanismen**, en klik vervolgens op **instellingen voor eenmalige aanmelding**.
    
    ![Beveiligingsmechanismen](./media/active-directory-saas-jobscience-tutorial/ic784364.png "beveiligingsmechanismen")

12. In Hallo **instellingen voor eenmalige aanmelding** sectie, voert u Hallo stappen te volgen:
    
    ![Eenmalige aanmelding instellingen](./media/active-directory-saas-jobscience-tutorial/ic781026.png "eenmalige aanmelding-instellingen")
    
    a. Selecteer **SAML ingeschakeld**.

    b. Klik op **Nieuw**.

13. Op Hallo **SAML Single Sign-On instelling bewerken** dialoogvenster Hallo volgende stappen uit te voeren:
    
    ![Afzonderlijke SAML aanmelding instelling](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML Single Sign-On-instelling")
    
    a. In Hallo **naam** textbox, typ een naam voor uw configuratie.

    b. In **verlener** textbox plakken Hallo-waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal.

    c. In Hallo **entiteit-Id** textbox type`https://salesforce-jobscience.com`

    d. Klik op **Bladeren** tooupload uw Azure AD-certificaat.

    e. Als **SAML identiteitstype**, selecteer **Assertion bevat Hallo Federatie-ID van het gebruikersobject Hallo**.

    f. Als **SAML identiteit locatie**, selecteer **identiteit is in Hallo NameIdentfier element van Hallo onderwerp instructie**.

    g. In **identiteit Provider aanmeldings-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.

    h. In **identiteit Provider afmelding URL** textbox plakken Hallo-waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.

    ik. Klik op **Opslaan**.

14. Op Hallo navigatiedeelvenster links in Hallo **beheren** sectie, klikt u op **domeinbeheer** tooexpand Hallo bijbehorende sectie en klik vervolgens op **mijn domein** tooopen hello  **Mijn domein** pagina. 
    
    ![Mijn domein](./media/active-directory-saas-jobscience-tutorial/ic767825.png "mijn domein")

15. Op Hallo **mijn domein** pagina in Hallo **aanmelding pagina huisstijl** sectie, klikt u op **bewerken**.
    
    ![Aanmeldingspagina huisstijl](./media/active-directory-saas-jobscience-tutorial/ic767826.png "aanmeldingspagina huisstijl")

16. Op Hallo **aanmelding pagina huisstijl** pagina in Hallo **verificatieservice** sectie, Hallo-naam van uw **SAML SSO instellingen** wordt weergegeven. Selecteer deze en klik vervolgens op **opslaan**.
    
    ![Aanmeldingspagina huisstijl](./media/active-directory-saas-jobscience-tutorial/ic784366.png "aanmeldingspagina huisstijl")

17. tooget hello SP eenmalige gestart op de aanmeldings-URL-Klik op Hallo **instellingen voor eenmalige aanmelding** in Hallo **beveiligingsmechanismen** sectie menu.

    ![Beveiligingsmechanismen](./media/active-directory-saas-jobscience-tutorial/ic784368.png "beveiligingsmechanismen")
    
    Klik op Hallo SSO profiel die u in de bovenstaande Hallo stap hebt gemaakt. Deze pagina bevat Hallo eenmalige aanmelding op de URL voor uw bedrijf (bijvoorbeeld [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).    

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobscience-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobscience-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobscience-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobscience-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-jobscience-test-user"></a>Een testgebruiker Jobscience maken

In de volgorde tooenable Azure AD gebruikers toolog in tooJobscience, moeten ze worden ingericht in Jobscience. In geval van Jobscience Hallo is inrichting een handmatige taak.

>[!NOTE]
>U kunt andere Jobscience gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Jobscience tooprovision Azure Active Directory-gebruikersaccounts.
>  
        
**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:**

1. Meld u bij tooyour **Jobscience** bedrijf site als administrator.

2. Ga tooSetup.
   
   ![Setup](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Setup")
3. Ga te**gebruikers beheren \> gebruikers**.
   
   ![Gebruikers](./media/active-directory-saas-jobscience-tutorial/ic784369.png "gebruikers")
4. Klik op **nieuwe gebruiker**.
   
   ![Alle gebruikers](./media/active-directory-saas-jobscience-tutorial/ic784370.png "alle gebruikers")
5. Op Hallo **-gebruiker bewerken** dialoogvenster Hallo volgende stappen uit te voeren:
   
   ![Gebruiker bewerken](./media/active-directory-saas-jobscience-tutorial/ic784371.png "gebruiker bewerken")
   
   a. In Hallo **voornaam** textbox, typ een naam van de eerste van de gebruiker Hallo zoals Britta.
   
   b. In Hallo **achternaam** textbox, typt u een achternaam van de gebruiker Hallo zoals Simon.
   
   c. In Hallo **Alias** textbox, typt u een aliasnaam van de gebruiker Hallo zoals brittas.

   d. In Hallo **e** textbox type Hallo e-mailadres van de gebruiker, zoals Brittasimon@contoso.com.

   e. In Hallo **gebruikersnaam** textbox, typ een naam van gebruiker, zoals Brittasimon@contoso.com.

   f. In Hallo **bijnaam** textbox, typ een naam nick van gebruiker zoals Simon.

   g. Klik op **Opslaan**.

    
> [!NOTE]
> Hello Azure Active Directory-accounthouder ontvangt een e-mailbericht en een koppeling tooconfirm volgt hun account voordat deze geactiveerd wordt.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooJobscience toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooJobscience, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Jobscience**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Jobscience tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Jobscience toepassing.
Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_203.png

