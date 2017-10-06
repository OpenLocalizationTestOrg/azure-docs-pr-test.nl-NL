---
title: 'Zelfstudie: Azure Active Directory-integratie met Teamphoria | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Teamphoria.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: f32be9742b76f7fe464036dadc108c62e4a787a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a>Zelfstudie: Azure Active Directory-integratie met Teamphoria

In deze zelfstudie leert u hoe toointegrate Teamphoria met Azure Active Directory (Azure AD).

Teamphoria integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooTeamphoria toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooTeamphoria (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with Teamphoria, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Teamphoria tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Teamphoria eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Teamphoria van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-teamphoria-from-hello-gallery"></a>Het toevoegen van Teamphoria van Hallo-galerie
tooconfigure hello integratie van Teamphoria in Azure AD, moet u tooadd Teamphoria uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Teamphoria via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Teamphoria**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. Selecteer in het deelvenster resultaten hello, **Teamphoria**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met Teamphoria op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Teamphoria is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Teamphoria toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Teamphoria.

tooconfigure en eenmalige aanmelding Azure AD-test met Teamphoria, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Teamphoria](#creating-a-teamphoria-test-user)**  -toohave een equivalent van Britta Simon in Teamphoria die is gekoppeld toohello Azure AD-weergave van haar.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding in uw toepassing Teamphoria configureren.

**Azure AD tooconfigure eenmalige aanmelding met Teamphoria, Voer Hallo stappen te volgen:**

1. In hello Azure Management portal op Hallo **Teamphoria** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. Op Hallo **Teamphoria domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    a. In Hallo **aanmeldings-URL** textbox type Hallo URL met Hallo patroon volgen:`https://<sub-domain>.teamphoria.com/login`  

    > [!NOTE] 
    > Houd er rekening mee dat deze niet Hallo echte waarden zijn. U hebt tooupdate deze waarden Hello werkelijke aanmeldings-URL. Neem contact op met [Teamphoria Client ondersteuningsteam](https://www.teamphoria.com/) tooget Hallo aanmelding URL. 

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla Hallo certificaat op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. Op Hallo **Teamphoria configuratie** sectie, klikt u op **configureren Teamphoria** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. tooconfigure eenmalige aanmelding op **Teamphoria** side, aanmelding tooyour Teamphoria toepassing als beheerder.

8. Ga te**BEHEERDERSINSTELLINGEN** optie in het linkerdeelvenster werkbalk Hallo en onder Hallo Hallo tabblad configureren, klikt u op **SINGLE SIGN-ON** venster tooopen Hallo SSO-configuratie.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. Klik op **IDENTITEITSPROVIDER toevoegen** optie op Hallo rechterbovenhoek tooopen Hallo formulier voor het Hallo-instellingen voor eenmalige aanmelding toe te voegen.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. Voer Hallo details in de velden Hallo beschreven onderstaande-

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamphoria-tutorial/Teamphoria_sso_save.png)

    a. **WEERGAVENAAM** : Voer Hallo weergavenaam van de invoegtoepassing Hallo op Hallo beheerpagina.

    b. **NAAM van de knop** : Hallo-naam van het Hallo-tabblad dat wordt weergegeven op de aanmeldingspagina Hallo voor logboekregistratie in via eenmalige aanmelding.

    c. **CERTIFICAAT** : Open Hallo certificaat eerder hebt gedownload van Azure-portal in Kladblok kopie Hallo inhoud Hallo Hallo dezelfde en plakt u deze hier in Hallo vak.

    d. **TOEGANGSPUNT** : plakken Hallo **SAML Single Sign-On Service-URL** gekopieerd eerdere formulier hello Azure-portal.

    e. Hallo-optie te schakelen**ON** en klik op **opslaan**. 

<!--### Next steps

tooensure users can sign-in tooTeamphoria after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooTeamphoria in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-teamphoria-test-user"></a>Een testgebruiker Teamphoria maken

In de volgorde tooenable Azure AD gebruikers toolog in Teamphoria, moeten ze worden ingericht in Teamphoria. In geval van Teamphoria Hallo is inrichting een handmatige taak.

**tooprovision een gebruikersaccounts uitvoeren Hallo volgende stappen:**

1. Aanmelden tooyour Teamphoria bedrijf site als beheerder.

2. Klik op **ADMIN** instellingen op de werkbalk van Hallo links en onder Hallo **beheren** Klik op tabblad **gebruikers** tooopen Hallo beheerpagina voor gebruikers.

    ![Werknemer toevoegen](./media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. Klik op Hallo **handmatig uit te NODIGEN** optie.

    ![Personen uitnodigen](./media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png)  

4. Uitvoeren na de actie op deze pagina. 
    
    ![Personen uitnodigen](./media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png)  

    a. In Hallo **e-MAILADRES** textbox Hallo **e-mailadres** van BrittaSimon.

    b. In Hallo **VOORNAAM** textbox type **Britta**.

    c. In Hallo **ACHTERNAAM** textbox type **Simon**.

    d. Klik op **uitnodiging 1 gebruiker**. Gebruiker moet tooaccept Hallo uitnodiging tooget in Hallo systeem gemaakt.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar tooTeamphoria toegang verlenen.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooTeamphoria, Voer Hallo stappen te volgen:**

1. Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Teamphoria**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u testen van uw instellingen voor eenmalige aanmelding wilt, opent u het toegangsvenster. Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png

