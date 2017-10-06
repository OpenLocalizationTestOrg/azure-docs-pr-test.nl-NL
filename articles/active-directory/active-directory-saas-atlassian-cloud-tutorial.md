---
title: 'Zelfstudie: Azure Active Directory-integratie met Atlassian Cloud | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Atlassian Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 729b8eb6-efc4-47fb-9f34-8998ca2c9545
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: f679e8b3306bf0efb9373d8baa0cfe095b760aaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atlassian-cloud"></a>Zelfstudie: Azure Active Directory-integratie met Atlassian Cloud

In deze zelfstudie leert u hoe toointegrate Atlassian Cloud met Azure Active Directory (Azure AD).

Atlassian Cloud integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooAtlassian Cloud heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooAtlassian Cloud (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Atlassian Cloud tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Atlassian Cloud eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Atlassian Cloud van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-atlassian-cloud-from-hello-gallery"></a>Het toevoegen van Atlassian Cloud van Hallo-galerie
tooconfigure hello integratie van Atlassian Cloud met Azure AD, moet u tooadd Atlassian Cloud uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Atlassian Cloud via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Atlassian Cloud**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_search.png)

5. Selecteer in het deelvenster resultaten hello, **Atlassian Cloud**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en test eenmalige aanmelding Azure AD met Atlassian Cloud op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in de Atlassian Cloud is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker in de Atlassian Cloud hello toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Atlassian Cloud.

tooconfigure en eenmalige aanmelding Azure AD-test met Atlassian Cloud, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Atlassian Cloud](#creating-an-atlassian-cloud-test-user)**  -toohave een equivalent van Britta Simon in Atlassian Cloud die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Atlassian Cloud.

**Voer tooconfigure Azure AD eenmalige aanmelding met Atlassian Cloud, Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Atlassian Cloud** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_samlbase.png)

3. Op Hallo **Atlassian Cloud-domein en de URL's** sectie, voert u Hallo volgende stappen uit als u wilt dat tooconfigure Hallo toepassing in **IDP** modus gestart:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url.png)

    a. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<instancename>.atlassian.net/admin/saml/edit`

    b. In Hallo **antwoord-URL** textbox, typ een URL als:`https://id.atlassian.com/login/saml/acs`

4. Controleer **weergeven geavanceerde instellingen voor URL** en uitvoeren van de volgende stap als u wilt dat tooconfigure Hallo toepassing in Hallo **SP** modus gestart:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url1.png)

    In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<instancename>.atlassian.net`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden met de werkelijke Hallo-id en de aanmeldings-URL. Hallo exacte waarden kunt u krijgen via Cloud SAML-configuratie van Atlassian scherm.
 
5. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_certificate.png) 

6. Op Hallo **Atlassian Cloudconfiguratie** sectie, klikt u op **Atlassian Cloud configureren** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_configure.png) 

7. tooget SSO is geconfigureerd voor uw toepassing, aanmelding toohello Atlassian Portal met behulp van Hallo administrator-rechten.

8. Klik in het Hallo-verificatiesectie van Hallo linkernavigatiebalk op **domeinen**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_06.png)

    a. Typ de naam van uw domein in Hallo tekstvak en klik vervolgens op **domein toevoegen**.
        
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_07.png)

    b. tooverify hello domein, klikt u op **controleren**. 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_08.png)

    c. Hallo-domein verificatie HTML-bestand downloaden, toohello hoofdmap van de website van uw domein te uploaden en klik vervolgens op **domein controleren**.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_09.png)

    d. Zodra het Hallo-domein is geverifieerd, waarde van Hallo Hallo **Status** veld is **geverifieerde**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_10.png)

9. Klik in het Hallo linkernavigatiebalk op **SAML**.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_11.png)

10. Maken van een SAML-configuratie en Hallo identiteit providerconfiguratie toevoegen.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_12.png)

    a. In Hallo **identiteitsprovider entiteit-ID** tekstvak plakken Hallo-waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.

    b. In Hallo **identiteitsprovider URL SSO** tekstvak plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.

    c. Open Hallo gedownload certificaat van de Azure portal en Hallo waarden kopiëren zonder Hallo Begin en einde regels en plak deze in Hallo **openbare X509 certificaat** vak.
    
    d. Klik op **configuratie opslaan** tooSave Hallo instellingen.
     
11. Werk hello Azure AD-instellingen toomake ervoor dat u setup Hallo identificatie-URL te corrigeren.
  
    a. Kopiëren Hallo **SP identiteit ID** van Hallo SAML scherm en plak deze in Azure AD als Hallo **id** waarde.

    b. Meld u op de URL is Hallo tenant-URL van uw Atlassian Cloud.     

     ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_13.png)
    
12. Klik in hello Azure-portal, op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_400.png)

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-an-atlassian-cloud-test-user"></a>Een testgebruiker Atlassian Cloud maken

Azure AD tooenable gebruikers toolog in tooAtlassian Cloud, ze in de Atlassian Cloud moeten worden ingericht.  
In geval van een Atlassian Cloud is inrichting een handmatige taak.

**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**

1. Klik in de beheersectie van de Site Hallo, op Hallo **gebruikers** knop

    ![Atlassian Cloud-gebruiker maken](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_14.png) 

2. Klik op Hallo **gebruiker maken** knop toocreate een gebruiker in Hallo Atlassian Cloud

    ![Atlassian Cloud-gebruiker maken](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_15.png) 

3. Voer van Hallo gebruiker **e-mailadres**, **gebruikersnaam**, en **volledige naam** en toegang tot de toepassing hello toewijzen. 

    ![Atlassian Cloud-gebruiker maken](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_16.png)
 
4. Klik op **gebruiker maken** knop, stuurt deze Hallo e-mailadres uitnodiging toohello gebruikersnaam en na het accepteren van Hallo uitnodiging Hallo gebruiker worden actief in Hallo-systeem. 

>[!NOTE] 
>U kunt ook maken Hallo bulksgewijs gebruikers door te klikken op Hallo **bulksgewijs maken** knop in Hallo sectie gebruikers.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooAtlassian Cloud.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooAtlassian Cloud, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Atlassian Cloud**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD SSO-configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Atlassian Cloud-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Atlassian Cloud-toepassing. Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_203.png

