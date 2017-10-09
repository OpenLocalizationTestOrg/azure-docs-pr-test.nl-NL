---
title: 'Zelfstudie: Azure Active Directory-integratie met de Jitbit Helpdesk | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Jitbit Helpdesk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ce27d4-0621-4103-8a34-e72c98d72ec3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 0f6c837bbb910c1e84f7ed9da676c5ab40f75338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jitbit-helpdesk"></a>Zelfstudie: Azure Active Directory-integratie met Jitbit Helpdesk

In deze zelfstudie leert u hoe toointegrate Jitbit Helpdesk met Azure Active Directory (Azure AD).

Jitbit Helpdesk integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooJitbit Helpdesk heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooJitbit Helpdesk (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met de Jitbit Helpdesk tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Jitbit Helpdesk eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Jitbit Helpdesk van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-jitbit-helpdesk-from-hello-gallery"></a>Het toevoegen van Jitbit Helpdesk van Hallo-galerie
tooconfigure hello integratie van Jitbit Helpdesk in Azure AD, moet u tooadd Jitbit Helpdesk uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Jitbit Helpdesk via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Jitbit Helpdesk**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_search.png)

5. Selecteer in het deelvenster resultaten hello, **Jitbit Helpdesk**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD met Jitbit Helpdesk op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Jitbit Helpdesk is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Jitbit Helpdesk toobe tot stand gebracht.

In Jitbit Helpdesk, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Jitbit Helpdesk, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Jitbit Helpdesk](#creating-a-jitbit-helpdesk-test-user)**  -toohave een equivalent van Britta Simon in Jitbit Helpdesk die gekoppelde toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Jitbit Helpdesk.

**Voer tooconfigure Azure AD eenmalige aanmelding met de Jitbit Helpdesk, Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Jitbit Helpdesk** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_samlbase.png)

3. Op Hallo **Jitbit Helpdesk domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen: 
    | |     
    | ----------------------------------------|
    | `https://<hostname>/helpdesk/User/Login`|
    | `https://<tenant-name>.Jitbit.com`|
    | |
    
    > [!NOTE] 
    > Deze waarde is geen echte. Deze waarde bijwerken Hello werkelijke aanmeldings-URL. Neem contact op met [Jitbit Helpdesk Client ondersteuningsteam](https://www.jitbit.com/support/) tooget deze waarde. 
    
    b.  In Hallo **id** textbox, typ een URL als volgt:`https://www.jitbit.com/web-helpdesk/`

    
 


4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_400.png)

6. Op Hallo **Jitbit Helpdesk configuratie** sectie, klikt u op **configureren Jitbit Helpdesk** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_configure.png) 

7. In een ander browservenster, meld u bij uw bedrijf Jitbit Helpdesk site als beheerder.

8. Klik in de werkbalk bovenaan Hallo Hallo op **beheer**.
   
    ![Beheer](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "beheer")

9. Klik op **algemene instellingen**.
   
    ![Gebruikers, bedrijven en machtigingen](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "gebruikers, bedrijven en machtigingen")

10. In Hallo **verificatie-instellingen** configuratie sectie, voert u Hallo stappen te volgen:
   
    ![Verificatie-instellingen](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "verificatie-instellingen")
    
    a. Selecteer **inschakelen-SAML één 2.0 aanmelden**, toosign in het gebruik van eenmalige aanmelding (SSO), met **OneLogin**.

    b. In Hallo **eindpunt-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.

    c. Open uw **base 64-** gecodeerd certificaat in Kladblok en kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **X.509-certificaat** tekstvak

    d. Klik op **wijzigingen opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox typenaam als **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-jitbit-helpdesk-test-user"></a>Maken van een testgebruiker Jitbit Helpdesk

In de volgorde tooenable Azure AD gebruikers toolog in Jitbit Helpdesk, moeten ze worden ingericht in Jitbit Helpdesk.  In geval van Jitbit Helpdesk Hallo is inrichting een handmatige taak.

**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**

1. Meld u bij tooyour **Jitbit Helpdesk** tenant.

2. Klik in het menu bovenaan Hallo Hallo **beheer**.
   
    ![Beheer](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "beheer")

3. Klik op **gebruikers, bedrijven en machtigingen**.
   
    ![Gebruikers, bedrijven en machtigingen](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "gebruikers, bedrijven en machtigingen")

4. Klik op **gebruiker toevoegen**.
   
    ![Gebruiker toevoegen](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "gebruiker toevoegen")
   
5. Typ in de sectie maken Hallo, Hallo-gegevens van hello Azure AD-account dat u wilt dat tooprovision als volgt:

    ![Maak](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "maken")
   
   a. In Hallo **gebruikersnaam** textbox type **BrittaSimon**, de gebruikersnaam Hallo zoals hello Azure-portal in.

   b. In Hallo **e** textbox type e-mailadres van de gebruiker hello, zoals  **BrittaSimon@contoso.com** .

   c. In Hallo **voornaam** textbox type voornaam van de gebruiker Hallo zoals **Britta**.

   d. In Hallo **achternaam** textbox type achternaam van de gebruiker Hallo zoals **Simon**.
   
   e. Klik op **Create**.

>[!NOTE]
>U kunt andere Jitbit Helpdesk gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Jitbit Helpdesk tooprovision Azure AD-gebruikersaccounts.
> 
        

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooJitbit Helpdesk.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooJitbit Helpdesk, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Jitbit Helpdesk**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Jitbit Helpdesk-tegel in Hallo Toegangsvenster, krijgt u de aanmeldingspagina van Jitbit Helpdesk-toepassing.
Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_203.png

