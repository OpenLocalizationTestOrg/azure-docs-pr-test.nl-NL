---
title: 'Zelfstudie: Azure Active Directory-integratie met Skillport | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Skillport.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4df349b2-a73f-4b88-a077-ec0fbfc26527
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: ba504c3cae5f92767eb90d8453887904690fe0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skillport"></a>Zelfstudie: Azure Active Directory-integratie met Skillport

In deze zelfstudie leert u hoe toointegrate Skillport met Azure Active Directory (Azure AD).

Skillport integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooSkillport toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooSkillport (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Skillport tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Skillport eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Skillport van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-skillport-from-hello-gallery"></a>Het toevoegen van Skillport van Hallo-galerie
tooconfigure hello integratie van Skillport in Azure AD, moet u tooadd Skillport uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Skillport via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. Klik op **nieuwe toepassing** knop op Hallo Hallo dialoogvenster bovenaan.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Skillport**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_search.png)

5. Selecteer in het deelvenster resultaten hello, **Skillport**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met Skillport op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Skillport is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Skillport toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Skillport.

tooconfigure en eenmalige aanmelding Azure AD-test met Skillport, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Skillport](#creating-a-skillport-test-user)**  -toohave een equivalent van Britta Simon in Skillport die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Skillport configureren.

**Azure AD tooconfigure eenmalige aanmelding met Skillport, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Skillport** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_samlbase.png)

3. Op Hallo **Skillport domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_url.png)

    a. In Hallo **aanmeldings-URL** textbox, type patronen u een URL met hello te volgen:
      
      EU Datacenter:`https://<subdomain>.skillport.eu`
   
      VS Datacenter:`https://<subdomain>.skillport.com`
   
    b. In Hallo **antwoord-URL** textbox, type patronen u een URL met hello te volgen:
    
      EU Datacenter:`https://<subdomain>.skillport.eu/adfs/ls/`
    
      VS Datacenter:`https://<subdomain>.skillport.com/sp/ACS.saml2`

    > [!NOTE] 
    > Deze waarden zijn niet Hallo echte. Deze waarden bijwerken met Hallo werkelijke antwoord-URL en de aanmeldings-URL. Neem contact op met [Skillport Client ondersteuningsteam](https://www.skillsoft.com/contact.asp) tooget deze waarden.
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skillport-tutorial/tutorial_general_400.png)

6. tooconfigure eenmalige aanmelding op **Skillport** zijde, moet u toosend Hallo gedownload **Metadata XML** te[Skillport ondersteuningsteam](https://www.skillsoft.com/contact.asp). Ze zullen het instellen van toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden.

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-skillport-tutorial/create_aaduser_01.png) 

2. Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-skillport-tutorial/create_aaduser_02.png) 

3. Bovenaan Hallo Hallo dialoogvenster, klikt u op **toevoegen** tooopen hello **gebruiker** dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-skillport-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-skillport-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-skillport-test-user"></a>Een testgebruiker Skillport maken

In de volgorde toocreate Skillport testgebruiker, moet u toocontact [Skillport ondersteuningsteam](https://www.skillsoft.com/contact.asp) als ze hebben meerdere bedrijfsscenario's op basis van de vereiste toohello van eindgebruiker. Ze wordt deze na overleg met de Hallo gebruikers configureren.  

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooSkillport toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooSkillport, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Skillport**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Skillport tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Skillport toepassing.
Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_203.png

