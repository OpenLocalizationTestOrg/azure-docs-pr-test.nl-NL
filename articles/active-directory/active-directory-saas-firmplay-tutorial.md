---
title: 'Zelfstudie: Azure Active Directory-integratie met FirmPlay - werknemer Advocacy voor werving | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en FirmPlay - werknemer Advocacy voor werving.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a6799629-7546-43f8-a966-956db32864b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: f143e0bb8f2a42de880d77e5f033694ce3f09cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-firmplay---employee-advocacy-for-recruiting"></a>Zelfstudie: Azure Active Directory-integratie met FirmPlay - werknemer Advocacy voor werving

In deze zelfstudie leert u hoe toointegrate FirmPlay - werknemer Advocacy voor werving met Azure Active Directory (Azure AD).

Integratie van FirmPlay - werknemer Advocacy voor werving met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooFirmPlay - werknemer Advocacy voor werving heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooFirmPlay - werknemer Advocacy voor werving (Single Sign-On) inschakelen met hun Azure AD-accounts
- U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

tooconfigure Azure AD-integratie met FirmPlay - werknemer Advocacy voor werving, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een FirmPlay - werknemer Advocacy voor het werven van eenmalige aanmelding ingeschakeld abonnement


> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.


tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. FirmPlay - werknemer Advocacy voor werving uit Hallo galerie toevoegen
2. Configureren en testen van Azure AD eenmalige aanmelding


## <a name="adding-firmplay---employee-advocacy-for-recruiting-from-hello-gallery"></a>FirmPlay - werknemer Advocacy voor werving uit Hallo galerie toevoegen
tooconfigure hello integratie van FirmPlay - werknemer Advocacy voor werving in Azure AD, moet u tooadd FirmPlay - werknemer Advocacy voor werving uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd FirmPlay - werknemer Advocacy voor werving via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **FirmPlay - werknemer Advocacy voor werving**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_001.png)

5. Selecteer in het deelvenster resultaten hello, **FirmPlay - werknemer Advocacy voor werving**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met FirmPlay - werknemer Advocacy voor werving op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in FirmPlay - werknemer Advocacy voor werving is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in FirmPlay - werknemer Advocacy voor werving toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in FirmPlay - werknemer Advocacy voor werving.

tooconfigure en eenmalige aanmelding Azure AD-test met FirmPlay - werknemer Advocacy voor werving, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een FirmPlay - werknemer Advocacy voor de testgebruiker werving](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)**  -toohave een equivalent van Britta Simon in FirmPlay: werknemer Advocacy voor het werven van die toohello Azure AD-weergave van haar gekoppeld.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding in uw FirmPlay - werknemer Advocacy voor werving toepassing configureren.

**tooconfigure eenmalige aanmelding Azure AD met FirmPlay - werknemer Advocacy voor werving, Voer Hallo stappen te volgen:**

1. In hello Azure Management portal op Hallo **FirmPlay - werknemer Advocacy voor werving** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_01.png)

3. Op Hallo **FirmPlay - werknemer Advocacy voor het werven van domein en de URL's** sectie in Hallo **aanmelding op URL** textbox, typ een URL met Hallo patroon volgen:`https://<your-subdomain>.firmplay.com/`

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_02.png)

    > [!NOTE] 
    > Houd er rekening mee dat dit geen Hallo echte waarde is. U hebt deze waarde Hello werkelijke aanmelden URL tooupdate. Neem contact op met [FirmPlay - werknemer Advocacy voor werving ondersteuningsteam](mailto:engineering@firmplay.com) tooget deze waarde. 

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **nieuw certificaat maken**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_03.png)   

5. Op Hallo **nieuw certificaat maken** dialoogvenster, klikt u op Hallo agenda-pictogram en selecteer een **vervaldatum**. Klik vervolgens op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-firmplay-tutorial/tutorial_general_300.png)

6. Op Hallo **SAML-certificaat voor ondertekening van** sectie **nieuwe certificaat activeren** en klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_04.png)

7. Op Hallo pop-upvenster **rollovercertificaat** venster, klikt u op **OK**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-firmplay-tutorial/tutorial_general_400.png)

8. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (base64)** en sla het Hallo-certificaatbestand op uw computer. 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_05.png) 

9. Op Hallo **FirmPlay - werknemer Advocacy voor configuratie werven** sectie, klikt u op **configureren FirmPlay - werknemer Advocacy voor werving** tooopen **configureren aanmelding**dialoogvenster.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_06.png) 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_07.png)

10. tooget SSO geconfigureerd voor uw toepassing, neem contact op met [FirmPlay - werknemer Advocacy voor werving ondersteuningsteam](mailto:engineering@firmplay.com) en voorzien Hallo volgende: 

    • Hallo gedownload **certificaatbestand**

    • Hallo **SAML Single Sign-On Service-URL**

    • Hallo **SAML entiteit-ID**

    • Hallo **Sign-Out URL**
  

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-firmplay-tutorial/create_aaduser_01.png) 

2. Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-firmplay-tutorial/create_aaduser_02.png) 

3. Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-firmplay-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-firmplay-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**. 



### <a name="creating-a-firmplay---employee-advocacy-for-recruiting-test-user"></a>Maken van een FirmPlay - werknemer Advocacy voor werving testgebruiker

In deze sectie kunt u een gebruiker Britta Simon aangeroepen in FirmPlay - werknemer Advocacy voor werving maken. Neem contact op met [FirmPlay - werknemer Advocacy voor werving ondersteuningsteam](mailto:engineering@firmplay.com) tooadd Hallo gebruikers in Hallo FirmPlay - werknemer Advocacy voor werving platform.


### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar toegang tooFirmPlay - werknemer Advocacy voor werving verlenen.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooFirmPlay - werknemer Advocacy voor werving, Voer Hallo stappen te volgen:**

1. Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **FirmPlay - werknemer Advocacy voor werving**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_50.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    


### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Wanneer u klikt op Hallo FirmPlay - werknemer Advocacy werving tegel in Hallo paneel voor Apptoegang, krijgt u automatisch aangemelde tooyour FirmPlay - werknemer Advocacy voor werving toepassing.


## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_203.png