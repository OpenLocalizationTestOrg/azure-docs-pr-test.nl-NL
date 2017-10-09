---
title: 'Zelfstudie: Azure Active Directory-integratie met Mozy Enterprise | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Mozy Enterprise.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 489b5e62-85c2-45c9-8766-326632d48114
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: bab0df4f3621b784cd8edfda3c8e10fe5a7ced9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mozy-enterprise"></a>Zelfstudie: Azure Active Directory-integratie met Mozy voor ondernemingen

In deze zelfstudie leert u hoe toointegrate Mozy Enterprise met Azure Active Directory (Azure AD).

Mozy-onderneming integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooMozy Enterprise heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooMozy Enterprise (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

tooconfigure Azure AD-integratie met Mozy voor ondernemingen, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Mozy Enterprise eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Mozy Enterprise van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-mozy-enterprise-from-hello-gallery"></a>Het toevoegen van Mozy Enterprise van Hallo-galerie
tooconfigure hello integratie van Mozy Enterprise in Azure AD, moet u tooadd Mozy Enterprise uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Mozy Enterprise via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Mozy Enterprise**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_search.png)

5. Selecteer in het deelvenster resultaten hello, **Mozy Enterprise**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD met Mozy ondernemingen op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in de onderneming Mozy is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker in de onderneming Mozy Hallo toobe tot stand gebracht.

In de onderneming Mozy, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en test eenmalige aanmelding Azure AD met Mozy voor ondernemingen, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Mozy Enterprise](#creating-a-mozy-enterprise-test-user)**  -toohave een equivalent van Britta Simon in Mozy onderneming die gekoppelde toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Mozy Enterprise.

**Voer tooconfigure Azure AD eenmalige aanmelding met Mozy Enterprise, Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Mozy Enterprise** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_samlbase.png)

3. Op Hallo **Mozy Enterprise domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_url.png)

    In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<tenantname>.Mozyenterprise.com`

    > [!NOTE] 
    > Deze waarde is geen echte. Deze waarde bijwerken Hello werkelijke aanmeldings-URL. Neem contact op met [Mozy Enterprise Client ondersteuningsteam](http://support.mozy.com/) tooget deze waarde.

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_400.png)

6. Op Hallo **Mozy Ondernemingsconfiguratie** sectie, klikt u op **configureren Mozy Enterprise** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_configure.png) 

7. In een ander browservenster, meld u bij uw bedrijf Mozy Enterprise site als beheerder.

8. In Hallo **configuratie** sectie, klikt u op **verificatiebeleid**.
   
   ![Verificatiebeleid](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "verificatiebeleid")

9. Op Hallo **verificatiebeleid** sectie, voert u Hallo stappen te volgen:
   
   ![Verificatiebeleid](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "verificatiebeleid")
   
   a. Selecteer **adreslijstservice** als **Provider**.
   
   b. Selecteer **Gebruik LDAP Push**.
   
   c. Klik op Hallo **SAML-verificatie** tabblad.
   
   d. Plakken **SAML Single Sign-On Service-URL**, die u hebt gekopieerd uit hello Azure-portal in Hallo **-URL voor webverificatie** textbox.
   
   e. Plakken **SAML entiteit-ID**, die u hebt gekopieerd uit hello Azure-portal in Hallo **SAML-eindpunt** textbox.
   
   f. De gedownloade base-64 gecodeerde certificaat Open in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak Hallo gehele certificaat in **SAML certificaat** textbox.
   
   g. Selecteer **eenmalige aanmelding inschakelen voor beheerders toolog met hun netwerkreferenties**.
   
   h. Klik op **wijzigingen opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-mozy-enterprise-test-user"></a>Maken van een testgebruiker Mozy Enterprise

In volgorde tooenable Azure AD gebruikers toolog in Mozy onderneming, moeten ze worden ingericht in Mozy onderneming. In geval van Mozy onderneming Hallo is inrichting een handmatige taak.

>[!NOTE]
>U kunt andere Mozy Enterprise gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Mozy Enterprise tooprovision AAD-gebruikersaccounts.

**tooprovision een gebruikersaccounts uitvoeren Hallo volgende stappen:**

1. Meld u bij tooyour **Mozy Enterprise** tenant.

2. Klik op **gebruikers**, en klik vervolgens op **nieuwe gebruiker toevoegen**.
   
   ![Gebruikers](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "gebruikers")
   
   >[!NOTE]
   >Hallo **nieuwe gebruiker toevoegen** optie wordt alleen weergegeven als **Mozy** is geselecteerd als de provider Hallo onder **verificatiebeleid**. Als SAML-verificatie is geconfigureerd, worden klikt u vervolgens Hallo gebruikers automatisch toegevoegd op de eerste aanmelding via eenmalige aanmelding op.
    
3. Uitvoeren op de nieuwe gebruikersdialoogvenster Hallo Hallo stappen te volgen:
   
   ![Gebruikers toevoegen](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "gebruikers toevoegen")
   
   a. Van Hallo **kiest u een groep** , selecteert u een groep.
   
   b. Van Hallo **wat voor soort gebruiker** , selecteert u een type.
   
   c. In Hallo **gebruikersnaam** textbox Hallo typenaam van hello Azure AD-gebruiker.
   
   d. In Hallo **e** textbox type Hallo e-mailadres van hello Azure AD-gebruiker.
   
   e. Selecteer **gebruiker instructie e-mail verzenden**.
   
   f. Klik op **toevoegen van gebruiker (s)**.

     >[!NOTE]
     > Na het maken van Hallo gebruiker een e-mailbericht verzonden toohello Azure AD-gebruiker met een account koppelen tooconfirm Hallo voordat deze geactiveerd wordt.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooMozy Enterprise.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooMozy Enterprise, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Mozy Enterprise**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Mozy Enterprise-tegel in Hallo Toegangsvenster, krijgt u de aanmeldingspagina Mozy bedrijfstoepassing.
Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_203.png

