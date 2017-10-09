---
title: 'Zelfstudie: Azure Active Directory-integratie met Gigya | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Gigya.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2c7d200b-9242-44a5-ac8a-ab3214a78e41
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 1992c5ad09b097563377a488fbf5a375f6511020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gigya"></a>Zelfstudie: Azure Active Directory-integratie met Gigya

In deze zelfstudie leert u hoe toointegrate Gigya met Azure Active Directory (Azure AD).

Gigya integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooGigya toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooGigya (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Gigya tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Gigya eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Gigya van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-gigya-from-hello-gallery"></a>Het toevoegen van Gigya van Hallo-galerie
tooconfigure hello integratie van Gigya in Azure AD, moet u tooadd Gigya uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Gigya via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Gigya**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_search.png)

5. Selecteer in het deelvenster resultaten hello, **Gigya**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met Gigya op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Gigya is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Gigya toobe tot stand gebracht.

Wijs in Gigya, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Gigya, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Gigya](#creating-a-gigya-test-user)**  -toohave een equivalent van Britta Simon in Gigya die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Gigya configureren.

**Azure AD tooconfigure eenmalige aanmelding met Gigya, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Gigya** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_samlbase.png)

3. Op Hallo **Gigya domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`http://<companyname>.gigya.com`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://fidm.gigya.com/saml/v2.0/<companyname>`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id. Neem contact op met [Gigya Client ondersteuningsteam](https://www.gigya.com/support-policy/) tooget deze waarden. 
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-gigya-tutorial/tutorial_general_400.png)

6. Op Hallo **Gigya configuratie** sectie, klikt u op **configureren Gigya** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_configure.png) 

7. In een ander browservenster, meld u bij uw bedrijf Gigya site als beheerder.

8. Ga te**instellingen \> SAML aanmelding**, en klik vervolgens op Hallo **toevoegen** knop.
   
    ![SAML-aanmelding](./media/active-directory-saas-gigya-tutorial/ic789532.png "SAML-aanmelding")

9. In Hallo **SAML aanmelding** sectie, voert u Hallo stappen te volgen:
   
    ![De SAML-configuratie](./media/active-directory-saas-gigya-tutorial/ic789533.png "SAML-configuratie")
   
    a. In Hallo **naam** textbox, typ een naam voor uw configuratie.
   
    b. In **verlener** textbox plakken Hallo-waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure Portal. 
   
    c. In **Single Sign-On Service-URL** textbox plakken Hallo-waarde van **Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure Portal.
   
    d. In **indeling naam-ID** textbox plakken Hallo-waarde van **indeling van de id** die u hebt gekopieerd vanuit Azure Portal.
   
    e. De base-64 gecodeerde certificaat openen in Kladblok gedownload vanuit Azure-portal kopie Hallo inhoud ervan naar het Klembord en plak deze toohello **X.509-certificaat** textbox.
   
    f. Klik op **instellingen opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-gigya-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-gigya-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-gigya-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-gigya-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-gigya-test-user"></a>Een testgebruiker Gigya maken

In de volgorde tooenable Azure AD gebruikers toolog in Gigya, moeten ze worden ingericht in Gigya.  
In geval van Gigya Hallo is inrichting een handmatige taak.

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a>tooprovision een gebruikersaccounts uitvoeren Hallo volgende stappen:

1. Meld u bij tooyour **Gigya** bedrijf site als beheerder.

2. Ga te**Admin \> gebruikers beheren**, en klik vervolgens op **gebruikers uitnodigen**.
   
    ![Gebruikers beheren](./media/active-directory-saas-gigya-tutorial/ic789535.png "gebruikers beheren")

3. Uitvoeren in het dialoogvenster Hallo gebruikers uitnodigen, Hallo stappen te volgen:
   
    ![Gebruikers uitnodigen](./media/active-directory-saas-gigya-tutorial/ic789536.png "gebruikers uitnodigen")
   
    a. In Hallo **e** textbox type Hallo e-mailalias op van een geldige Azure Active Directory-account dat u wilt dat tooprovision.
    
    b. Klik op **gebruiker uitnodigen**.
      
    > [!NOTE]
    > Hello Azure Active Directory-accounthouder ontvangt een e-mailbericht met een account koppelen tooconfirm Hallo voordat deze geactiveerd wordt.
    > 
    

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooGigya toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooGigya, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Gigya**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.

Als u op Hallo Gigya tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Gigya toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_203.png

