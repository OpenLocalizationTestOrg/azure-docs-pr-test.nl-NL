---
title: 'Zelfstudie: Azure Active Directory-integratie met Samanage | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Samanage.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0db4fb0-7eec-48c2-9c7a-beab1ab49bc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c8edc29f113b8088438618a731e97c0f4f155b9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-samanage"></a>Zelfstudie: Azure Active Directory-integratie met Samanage

In deze zelfstudie leert u hoe toointegrate Samanage met Azure Active Directory (Azure AD).

Samanage integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooSamanage toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooSamanage (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Samanage tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Samanage eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Samanage van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-samanage-from-hello-gallery"></a>Het toevoegen van Samanage van Hallo-galerie
tooconfigure hello integratie van Samanage in Azure AD, moet u tooadd Samanage uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Samanage via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Samanage**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_search.png)

5. Selecteer in het deelvenster resultaten hello, **Samanage**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met Samanage op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Samanage is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Samanage toobe tot stand gebracht.

Wijs in Samanage, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Samanage, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Samanage](#creating-a-samanage-test-user)**  -toohave een equivalent van Britta Simon in Samanage die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Samanage configureren.

**Azure AD tooconfigure eenmalige aanmelding met Samanage, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Samanage** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_samlbase.png)

3. Op Hallo **Samanage domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<Company Name>.samanage.com/saml_login/<Company Name>`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<Company Name>.samanage.com`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Deze waarden bijwerken met Hallo werkelijke aanmeldings-URL en de id, die verderop in Hallo zelfstudie wordt uitgelegd. Voor meer informatie contact op met [Samanage Client ondersteuningsteam](https://www.samanage.com/support).    
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samanage-tutorial/tutorial_general_400.png)

6. Op Hallo **Samanage configuratie** sectie, klikt u op **configureren Samanage** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out-URL en de entiteit-ID SAML** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_configure.png) 

7. In een ander browservenster, meld u bij uw bedrijf Samanage site als beheerder.

8. Klik op **Dashboard** en selecteer **Setup** in het navigatiedeelvenster links.
   
    ![Dashboard](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Dashboard")

9. Klik op **Single Sign-On**.
   
    ![Eenmalige aanmelding](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "eenmalige aanmelding")

10. Navigeer te**aanmelding via SAML** sectie, voert u Hallo stappen te volgen:
   
    ![Aanmelding via SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "aanmelding via SAML")
 
    a. Klik op **eenmalige aanmelding met SAML inschakelen**.  
 
    b. In Hallo **identiteit Provider URL** textbox plakken Hallo-waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.    
 
    c. Hallo bevestigen **aanmeldings-URL** komt overeen met Hallo **aanmelding op URL** van **Samanage domein en de URL's** sectie in Azure-portal.
 
    d. In Hallo **afmelding URL** textbox Hallo waarde **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.
 
    e. In Hallo **SAML verlener** textbox type Hallo app id URI instellen in de id-provider.
 
    f. Open uw base-64 gecodeerde certificaat gedownload vanuit Azure-portal in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **plak uw id-Provider-x.509-certificaat onderstaande** textbox.
 
    g. Klik op **gebruikers maken als ze bestaan niet in Samanage**.
 
    h. Klik op **Update**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
 
### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samanage-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samanage-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samanage-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samanage-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-samanage-test-user"></a>Een testgebruiker Samanage maken

Azure AD tooenable gebruikers toolog in tooSamanage, ze in Samanage moeten worden ingericht.  
In geval van Samanage Hallo is inrichting een handmatige taak.

**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**

1. Meld u aan bij uw bedrijf Samanage site als beheerder.

2. Klik op **Dashboard** en selecteer **Setup** in het linkernavigatievenster pan.
   
    ![Setup](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Setup")

3. Klik op Hallo **gebruikers** tabblad
   
    ![Gebruikers](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "gebruikers")

4. Klik op **nieuwe gebruiker**.
   
    ![Nieuwe gebruiker](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "nieuwe gebruiker")

5. Type Hallo **naam** en Hallo **e-mailadres** van een Azure Active Directory-account u wilt tooprovision en op **gebruiker maken**.
   
    ![Gebruiker maken](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "gebruiker maken")
   
   >[!NOTE]
   >Hello Azure Active Directory-accounthouder wordt een e-mailbericht ontvangen en volg een koppeling tooconfirm hun account maken voordat deze geactiveerd wordt. U kunt andere Samanage gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Samanage tooprovision Azure Active Directory-gebruikersaccounts.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooSamanage toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooSamanage, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Samanage**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Samanage tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Samanage toepassing.
Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_203.png

