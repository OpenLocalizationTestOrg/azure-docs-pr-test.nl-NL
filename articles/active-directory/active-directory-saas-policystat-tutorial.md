---
title: 'Zelfstudie: Azure Active Directory-integratie met PolicyStat | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en PolicyStat.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: af5eb0f1-1c8e-4809-b0c4-8ccfb915ca42
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 868053cd0d37359fd9b4aeb93dba42cbbaa09845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-policystat"></a>Zelfstudie: Azure Active Directory-integratie met PolicyStat

In deze zelfstudie leert u hoe toointegrate PolicyStat met Azure Active Directory (Azure AD).

PolicyStat integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooPolicyStat toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooPolicyStat (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met PolicyStat tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een PolicyStat eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van PolicyStat van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-policystat-from-hello-gallery"></a>Het toevoegen van PolicyStat van Hallo-galerie
tooconfigure hello integratie van PolicyStat in Azure AD, moet u tooadd PolicyStat uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd PolicyStat via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **PolicyStat**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_search.png)

5. Selecteer in het deelvenster resultaten hello, **PolicyStat**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met PolicyStat op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in PolicyStat is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in PolicyStat toobe tot stand gebracht.

Wijs in PolicyStat, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met PolicyStat, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker PolicyStat](#creating-a-policystat-test-user)**  -toohave een equivalent van Britta Simon in PolicyStat die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing PolicyStat configureren.

**Azure AD tooconfigure eenmalige aanmelding met PolicyStat, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **PolicyStat** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_samlbase.png)

3. Op Hallo **PolicyStat domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.policystat.com`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.policystat.com/saml2/metadata/`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id. Neem contact op met [PolicyStat Client ondersteuningsteam](http://www.policystat.com/support/) tooget deze waarden. 
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_certificate.png) 

5. Hallo-doel van deze sectie is toooutline hoe tooenable gebruikers tooauthenticate tooPolicyStat aan hun account in Azure AD dat gebruikmaakt van Federatie gebaseerd op Hallo SAML-protocol.

    Hallo PolicyStat toepassing hello SAML asserties verwacht in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen tooyour **SAML-Token kenmerken** configuratie.  

     Hallo volgende Schermafbeelding toont een voorbeeld hiervan.

     ![Kenmerken](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "kenmerken")

6. Kenmerktoewijzingen tooadd Hallo vereist, voert u Hallo stappen te volgen:

    | Naam van kenmerk    |   De waarde van kenmerk |
    |------------------- | -------------------- |
    | UID | ExtractMailPrefix([mail]) |
    
    a. Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addatribute.png)
    
    b. In Hallo **kenmerknaam** textbox type **uid**.

    c. In Hallo **kenmerkwaarde** textbox, selecteer **ExtractMailPrefix()**.    
   
    d. Van Hallo **Mail** selecteert **User.mail**.
    
    e. Klik op **Ok**

7. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-policystat-tutorial/tutorial_general_400.png)

8. In een ander browservenster, meld u bij uw bedrijf PolicyStat site als beheerder.

9. Klik op Hallo **Admin** tabblad en klik vervolgens op **configuratie voor één aanmelding** in het navigatiedeelvenster links.
   
    ![Menu beheerder](./media/active-directory-saas-policystat-tutorial/ic808633.png "Menu beheerder")

10. In Hallo **Setup** sectie **inschakelen eenmalige aanmelding integratie**.
   
    ![Eenmalige aanmelding configuratie](./media/active-directory-saas-policystat-tutorial/ic808634.png "Single Sign-On-configuratie")

11. Klik op **kenmerken configureren**, en klikt u op Hallo **kenmerken configureren** sectie, voert u Hallo stappen te volgen:
   
    ![Eenmalige aanmelding configuratie](./media/active-directory-saas-policystat-tutorial/ic808635.png "Single Sign-On-configuratie")
   
    a. In Hallo **kenmerk Username** textbox type **uid**.

    b. In Hallo **voornaam kenmerk** textbox type **firstname** van gebruiker **Britta**.

    c. In Hallo **laatste naamkenmerk** textbox type **lastname** van gebruiker **Simon**.

    d. In Hallo **e kenmerk** textbox type **emailaddress** van gebruiker  **BrittaSimon@contoso.com** .

    e. Klik op **wijzigingen opslaan**.

12. Klik op **uw IDP metagegevens**, en klikt u op Hallo **uw IDP metagegevens** sectie, voert u Hallo stappen te volgen:
   
    ![Eenmalige aanmelding configuratie](./media/active-directory-saas-policystat-tutorial/ic808636.png "Single Sign-On-configuratie")
   
    a. Open uw gedownloade metagegevensbestand, kopie Hallo inhoud en plak deze in Hallo **uw identiteit Provider metagegevens** textbox.

    b. Klik op **wijzigingen opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-policystat-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-policystat-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-policystat-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-policystat-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-policystat-test-user"></a>Een testgebruiker PolicyStat maken

In de volgorde tooenable Azure AD gebruikers toolog in PolicyStat, moeten ze worden ingericht in PolicyStat.  

PolicyStat ondersteunt alleen in de tijd van gebruikersinrichting. Dit betekent dat, hoeft u geen tooadd Hallo gebruikers handmatig tooPolicyStat. Hallo gebruikers krijgen op hun eerste aanmelding via eenmalige aanmelding automatisch toegevoegd.

>[!NOTE]
>U kunt andere PolicyStat gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door PolicyStat tooprovision Azure AD-gebruikersaccounts.
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooPolicyStat toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooPolicyStat, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **PolicyStat**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo PolicyStat tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour PolicyStat toepassing.
Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_203.png

