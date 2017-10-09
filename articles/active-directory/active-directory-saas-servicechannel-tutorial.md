---
title: 'Zelfstudie: Azure Active Directory-integratie met ServiceChannel | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en ServiceChannel.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c3546eab-96b5-489b-a309-b895eb428053
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/3/2017
ms.author: jeedes
ms.openlocfilehash: 956371a1e99dcba4137c271ecfe8a62b9ec64a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicechannel"></a>Zelfstudie: Azure Active Directory-integratie met ServiceChannel

In deze zelfstudie leert u hoe toointegrate ServiceChannel met Azure Active Directory (Azure AD).

ServiceChannel integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooServiceChannel toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooServiceChannel (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met ServiceChannel tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een ServiceChannel eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van ServiceChannel van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-servicechannel-from-hello-gallery"></a>Het toevoegen van ServiceChannel van Hallo-galerie
tooconfigure hello integratie van ServiceChannel in Azure AD, moet u tooadd ServiceChannel uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd ServiceChannel via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **ServiceChannel**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_000.png)

5. Selecteer in het deelvenster resultaten hello, **ServiceChannel**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_2.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met ServiceChannel op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in ServiceChannel is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in ServiceChannel toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in ServiceChannel.

tooconfigure en test eenmalige aanmelding Azure AD met behulp van ServiceChannel, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker ServiceChannel](#creating-a-servicechannel-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding in uw toepassing ServiceChannel configureren.

**Azure AD tooconfigure eenmalige aanmelding met ServiceChannel, Voer Hallo stappen te volgen:**

1. In hello Azure Management portal op Hallo **ServiceChannel** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_01.png)

3. Op Hallo **ServiceChannel-domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_urls.png)

    a. In Hallo **id** textbox Hallo typewaarde als:`http://adfs.<domain>.com/adfs/service/trust`

    b. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<customer domain>.servicechannel.com/saml/acs`

    > [!NOTE] 
    > Houd er rekening mee dat deze niet Hallo echte waarden zijn. U hebt deze waarden door de werkelijke id en de antwoord-URL Hallo tooupdate. We raden hier u toouse Hallo unieke waarde van een tekenreeks in Hallo id. Neem contact op met [ServiceChannel ondersteuningsteam](https://servicechannel.zendesk.com/hc/en-us) tooget deze waarden.

4. Uw toepassing ServiceChannel verwacht Hallo SAML asserties in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen tooyour SAML-token kenmerken-configuratie is vereist. Hallo volgende Schermafbeelding toont een voorbeeld voor deze. **NameIdentifier (gebruikers-id)** is alleen verplichte claim Hallo en Hallo standaardwaarde is **user.userprincipalname** maar ServiceChannel verwacht deze toegewezen met toobe **user.mail**. Als u van plan bent tooenable NET In Time gebruikers inrichten, moet u Hallo claims zoals hieronder wordt weergegeven na toevoegen. **Rol** claim moet toobe te toegewezen**user.assignedroles** die Hallo-rol van Hallo gebruiker bevat.  

    U kunt verwijzen ServiceChannel handleiding [hier](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) voor meer informatie over claims.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_attribute.png)

    > [!NOTE] 
    > Klik op de [hier](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) tooknow hoe tooconfigure **rol** in Azure AD

5. In **gebruikerskenmerken** sectie, klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** en Hallo kenmerken instellen.

    | Naam van kenmerk | De waarde van kenmerk |
    | --- | --- |    
    | Rol| User.assignedroles |

    a. Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_05.png)
    
    b. In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.
    
    c. Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.
    
    d. Klik op **Ok**
    
6. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_05.png) 

7. Klik op **Opslaan**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicechannel-tutorial/tutorial_general_400.png)

8. Op Hallo **ServiceChannel configuratie** sectie, klikt u op **configureren ServiceChannel** tooopen **eenmalige aanmelding configureren** venster. Houd er rekening mee Hallo **SAML Enitity ID** van Hallo **Naslaggids** sectie.

9. tooconfigure eenmalige aanmelding op **ServiceChannel** zijde, moet u toosend Hallo gedownload **certificaat (Base64)** en **SAML entiteit-ID** te[ Het ondersteuningsteam van ServiceChannel](https://servicechannel.zendesk.com/hc/en-us). Ze stelt deze in volgorde toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden.

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_01.png) 

2. Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_02.png) 

3. Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**. 

### <a name="creating-a-servicechannel-test-user"></a>Een testgebruiker ServiceChannel maken

Toepassing ondersteunt Just in tijd gebruikers inrichten en na verificatie gebruikers wordt in de toepassing hello automatisch gemaakt. Voor volledige gebruikersinrichting, neem contact op met [ondersteuningsteam ServiceChannel](https://servicechannel.zendesk.com/hc/en-us)

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar tooServiceChannel toegang verlenen.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooServiceChannel, Voer Hallo stappen te volgen:**

1. Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **ServiceChannel**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_app01.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo ServiceChannel-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour ServiceChannel-toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_203.png