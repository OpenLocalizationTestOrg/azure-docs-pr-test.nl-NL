---
title: 'Zelfstudie: Azure Active Directory-integratie met Procore SSO | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Procore eenmalige aanmelding.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9818edd3-48c0-411d-b05a-3ec805eafb2e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: bb918617f18ba3f44ddde469e6fc411977752f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-procore-sso"></a>Zelfstudie: Azure Active Directory-integratie met Procore SSO

In deze zelfstudie leert u hoe toointegrate Procore eenmalige aanmelding bij Azure Active Directory (Azure AD).

Procore SSO integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooProcore eenmalige aanmelding heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooProcore SSO (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with Procore SSO, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Procore SSO.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Vereisten

tooconfigure Azure AD-integratie met Procore SSO, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Procore SSO eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Procore SSO van hello galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-procore-sso-from-hello-gallery"></a>Het toevoegen van Procore SSO van hello galerie
tooconfigure hello integratie van Procore SSO in Azure AD, moet u tooadd Procore SSO van hello galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Procore eenmalige aanmelding via Hallo gallery Hallo stappen uitvoeren:**

1. In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Procore SSO**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_search.png)

5. Selecteer in het deelvenster resultaten hello, **Procore SSO**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met Procore eenmalige aanmelding op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Procore SSO is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Procore SSO toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Procore eenmalige aanmelding.

tooconfigure en eenmalige aanmelding Azure AD-test met Procore SSO, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Procore SSO](#creating-a-procore-sso-test-user)**  -toohave een equivalent van Britta Simon in Procore eenmalige aanmelding die is gekoppeld toohello Azure AD-weergave van haar.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding configureren in uw toepassing Procore eenmalige aanmelding.

**Voer tooconfigure Azure AD eenmalige aanmelding met Procore SSO Hallo stappen te volgen:**

1. In hello Azure Management portal op Hallo **Procore SSO** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_samlbase.png)

3. Op Hallo **Procore SSO-domein en de URL's** sectie, hello gebruiker beschikt niet over tooperform eventuele stappen zoals Hallo app al vooraf is geïntegreerd met Azure.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_url.png)

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/tutorial_general_400.png)

6. Op Hallo **Procore SSO configuratie** sectie, klikt u op **Procore eenmalige aanmelding configureren** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_configure.png) 

7. tooconfigure eenmalige aanmelding op **Procore SSO** side, aanmelding tooyour procore bedrijf site als beheerder.

8. In Hallo werkset vervolgkeuzelijst omlaag, klikt u op **Admin** tooopen Hallo SSO instellingenpagina.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/procore_tool_admin.png)

9. Hallo-waarden in de vakken Hallo als plakken beschreven onderstaande-

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/procore_setting_admin.png)    

    a. In Hallo **eenmalige aanmelding op URL-verlener** vak, plak Hallo SAML entiteit-ID opgehaald uit hello Azure-portal.

    b. In Hallo **SAML aanmelding op de doel-URL** vak, plak Hallo SAML Single Sign-On Service-URL is gekopieerd uit hello Azure-portal.

    c. Open nu Hallo **Metadata XML** gedownloade hierboven van hello Azure-portal en kopiëren Hallo certificaat in het Hallo-tag met de naam **X509Certificate**. Plakken Hallo waarde gekopieerd naar Hallo **certificaat voor eenmalige aanmelding x509** vak.

10. Klik op **wijzigingen opslaan**.

11. Na deze instellingen moet u toosend hello **domeinnaam** (bijvoorbeeld **contoso.com**) via die u aan te bij Procore toohello melden [Procore ondersteuningsteam](https://support.procore.com/) en deze zullen activeren van federatieve SSO voor dat domein.

<!--### Next steps

tooensure users can sign-in tooProcore SSO after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Procore SSO prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooProcore SSO in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Procore SSO users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-procoresso-tutorial/create_aaduser_01.png) 

2. Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-procoresso-tutorial/create_aaduser_02.png) 

3. Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-procoresso-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-procoresso-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-procore-sso-test-user"></a>Maken van een testgebruiker Procore SSO

Volg Hallo onderstaande stappen toocreate een Procore testgebruiker op hun kant.

1. Aanmelding tooyour procore bedrijf site als beheerder.  

2. In Hallo werkset vervolgkeuzelijst omlaag, klikt u op **Directory** tooopen Hallo bedrijf directory-pagina.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/Procore_sso_directory.png)

3. Klik op **toevoegen van een persoon** optie tooopen Hallo formulier en voert u na de opties - uitvoeren

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/Procore_user_add.png)

    a. In Hallo **voornaam** tekstvak de voornaam van de gebruiker van het type zoals **Britta**.

    b. In Hallo **achternaam** tekstvak de achternaam van de gebruiker van het type zoals **Simon**.

    c. In Hallo **e-mailadres** textbox e-mailadres van de gebruiker van het type, zoals  **BrittaSimon@contoso.com** .

    d. Selecteer **machtigingssjabloon** als **machtigingssjabloon Later toepassen**.

    e. Klik op **Create**.

4. Controleer de details en bijwerken Hallo voor toegevoegde Neem contact op met de Hallo.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/Procore_user_check.png)

5. Klik op **opslaan en verzenden Invitiation** (als een uitnodiging via e-mail vereist is) of **opslaan** (rechtstreeks opslaan) toocomplete Hallo gebruikersregistratie.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/Procore_user_save.png)    

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar toegang tooProcore SSO verlenen.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooProcore SSO, Voer Hallo stappen te volgen:**

1. Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Procore SSO**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u testen van uw instellingen voor eenmalige aanmelding wilt, opent u het toegangsvenster. Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586). Als u op Hallo Procore SSO-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Procore SSO-toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_203.png

