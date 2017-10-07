---
title: 'Zelfstudie: Azure Active Directory-integratie met PlanMyLeave | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en PlanMyLeave.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b0d31cbe-7ae2-488b-9cf3-4927391fa744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: 44a6782e44ef22fc957544960be1742f9eed6e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-planmyleave"></a>Zelfstudie: Azure Active Directory-integratie met PlanMyLeave

In deze zelfstudie leert u hoe toointegrate PlanMyLeave met Azure Active Directory (Azure AD).

PlanMyLeave integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooPlanMyLeave toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooPlanMyLeave (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met PlanMyLeave tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een PlanMyLeave eenmalige aanmelding ingeschakeld abonnement


> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.


tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van PlanMyLeave van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding


## <a name="adding-planmyleave-from-hello-gallery"></a>Het toevoegen van PlanMyLeave van Hallo-galerie
tooconfigure hello integratie van PlanMyLeave in Azure AD, moet u tooadd PlanMyLeave uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd PlanMyLeave via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **PlanMyLeave**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_001.png)

5. Selecteer in het deelvenster resultaten hello, **PlanMyLeave**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met PlanMyLeave op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in PlanMyLeave is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in PlanMyLeave toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in PlanMyLeave.

tooconfigure en eenmalige aanmelding Azure AD-test met PlanMyLeave, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker PlanMyLeave](#creating-a-planmyleave-test-user)**  -toohave een equivalent van Britta Simon in PlanMyLeave die is gekoppeld toohello Azure AD-weergave van haar.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding in uw toepassing PlanMyLeave configureren.

**Azure AD tooconfigure eenmalige aanmelding met PlanMyLeave, Voer Hallo stappen te volgen:**

1. In hello Azure Management portal op Hallo **PlanMyLeave** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster pagina als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_01.png)

3. Op Hallo **PlanMyLeave domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_02.png)

    a. In Hallo **aanmelding op URL** textbox, typ een URL met Hallo patroon volgen:`https://<company-name>.planmyleave.com/Login.aspx`
    
    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<company-name>.planmyleave.com`

    > [!NOTE] 
    > Houd er rekening mee dat deze niet Hallo echte waarden zijn. U hebt deze waarden Hello werkelijke Meld u aan bij de URL en de id tooupdate. Neem contact op met [PlanMyLeave ondersteuningsteam](mailto:support@planmyleave.com) tooget deze waarden.

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **nieuw certificaat maken**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_03.png)     

5. Op Hallo **nieuw certificaat maken** dialoogvenster, klikt u op Hallo agenda-pictogram en selecteer een **vervaldatum**. Klik vervolgens op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_300.png)

6. Op Hallo **SAML-certificaat voor ondertekening van** sectie **nieuwe certificaat activeren** en klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_04.png)

7. Op Hallo pop-upvenster **rollovercertificaat** venster, klikt u op **OK**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_400.png)

8. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_05.png) 

9. Op Hallo **PlanMyLeave configuratie** sectie, klikt u op **configureren PlanMyLeave** tooopen **eenmalige aanmelding configureren** venster.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_06.png) 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_07.png)

10. Meld u aan bij uw tenant PlanMyLeave als een beheerder in een ander browservenster.

11. Ga te**Setup van System**. Klik op Hallo **beveiligingsbeheer** sectie Klik **bedrijf SAML-instellingen** .

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_002.png) 

12. Op Hallo **SAML instellingen** sectie, klikt u op het pictogram van de editor.

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_003.png)

13. Op Hallo **SAML-Update-instellingen** sectie, voert u Hallo stappen te volgen:

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_004.png)

    a.  In Hallo **aanmeldings-URL** textbox Hallo-waarde van **SAML Single Sign-On Service-URL** van het venster voor configuratie van Azure AD-toepassing.

    b.  Open uw gedownloade certificaat-bestand in Kladblok, alleen Hallo inhoud tussen Hallo---begint certificaat--- en---einde certificaat---ervan naar het Klembord kopiëren en plak deze toohello **certificaat** textbox.

    c. Instellen'**Is ingeschakeld**'te'**Ja**'.

    d. Klik op **Opslaan**.



### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_01.png) 

2. Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_02.png) 

3. Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**. 



### <a name="creating-a-planmyleave-test-user"></a>Een testgebruiker PlanMyLeave maken

Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in PlanMyLeave van een gebruiker. PlanMyLeave ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.

Er is geen actie-item voor u in deze sectie. Een nieuwe gebruiker wordt tijdens een poging tooaccess PlanMyLeave gemaakt als deze nog niet bestaat.

> [!NOTE]
> Als u een gebruiker toocreate handmatig nodig hebt, moet u toocontact [PlanMyLeave ondersteuningsteam](mailto:support@planmyleave.com).



### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar tooPlanMyLeave toegang verlenen.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooPlanMyLeave, Voer Hallo stappen te volgen:**

1. Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **PlanMyLeave**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_50.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    


### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo PlanMyLeave tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour PlanMyLeave toepassing.


## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_203.png