---
title: 'Zelfstudie: Azure Active Directory-integratie met ArcGIS Online | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding van Azure Active Directory en ArcGIS Online.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9e132a4-29e7-48bf-beb9-4148e617c8a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: f3dd55d798cf3256fb2758e011f33946baa405ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-online"></a>Zelfstudie: Azure Active Directory-integratie met ArcGIS Online

In deze zelfstudie leert u hoe toointegrate ArcGIS Online met Azure Active Directory (Azure AD).

Online ArcGIS integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die Online tooArcGIS toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooArcGIS Online (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with ArcGIS Online, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in ArcGIS Online.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met ArcGIS Online tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een ArcGIS Online eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Online ArcGIS van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-arcgis-online-from-hello-gallery"></a>Het toevoegen van Online ArcGIS van Hallo-galerie
tooconfigure hello integratie ArcGIS online met Azure AD, moet u tooadd ArcGIS Online uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd ArcGIS Online via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. Klik op **nieuwe toepassing** knop bovenaan Hallo van Hallo dialoogvenster tooadd nieuwe toepassing.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **ArcGIS Online**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_search.png)

5. Selecteer in het deelvenster resultaten hello, **ArcGIS Online**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met ArcGIS Online op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in ArcGIS Online is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante Hallo-gebruiker in ArcGIS Online toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** ArcGIS Online.

tooconfigure en test eenmalige aanmelding Azure AD met ArcGIS Online, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een Online ArcGIS testgebruiker](#creating-an-arcgis-online-test-user)**  -toohave een equivalent van Britta Simon in ArcGIS Online die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing ArcGIS Online configureren.

**Voer tooconfigure Azure AD eenmalige aanmelding met Online ArcGIS, Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **ArcGIS Online** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_samlbase.png)

3. Op Hallo **ArcGIS Online domein en de URL's** sectie, voert u Hallo stap:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_url.png)

    In Hallo **aanmeldings-URL** textbox Hallo typewaarde met Hallo patroon volgen:`https://<company>.maps.arcgis.com`

    > [!NOTE] 
    > Deze waarde is geen echte Hallo. Deze waarde bijwerken Hello werkelijke aanmeldings-URL. Neem contact op met [ArcGIS Online Client ondersteuningsteam](http://support.esri.com/) tooget deze waarde. 

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-arcgis-tutorial/tutorial_general_400.png)

6. In een ander browservenster, meld u bij uw bedrijf ArcGIS site als beheerder.

7. Klik op **bewerken van instellingen**.

    ![Instellingen bewerken](./media/active-directory-saas-arcgis-tutorial/ic784742.png "instellingen bewerken")

8. Klik op **beveiliging**.

    ![Beveiliging](./media/active-directory-saas-arcgis-tutorial/ic784743.png "beveiliging")

9. Onder **Enterprise aanmeldingen**, klikt u op **IDENTITEITSPROVIDER ingesteld**.

    ![Enterprise-aanmeldingen](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Enterprise-aanmeldingen")

10. Op Hallo **identiteitsprovider ingesteld** configuratie pagina, voert u Hallo stappen te volgen:
   
    ![Instellen van de identiteitsprovider](./media/active-directory-saas-arcgis-tutorial/ic784745.png "identiteitsprovider instellen")
   
    a. In Hallo **naam** textbox, typ de naam van uw organisatie.

    b. Voor **metagegevens voor Hallo Enterprise-id-Provider worden opgegeven met behulp van**, selecteer **een bestand**.

    c. tooupload uw gedownloade metagegevensbestand, klikt u op **bestand kiezen**.

    d. Klik op **SET IDENTITEITSPROVIDER**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-arcgis-tutorial/create_aaduser_01.png) 

2. Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-arcgis-tutorial/create_aaduser_02.png) 

3. Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-arcgis-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-arcgis-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van Britta Simon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-an-arcgis-online-test-user"></a>Maken van een Online ArcGIS testgebruiker

In volgorde tooenable Azure AD gebruikers toolog in ArcGIS Online, moeten ze worden ingericht in ArcGIS Online.  
In geval van ArcGIS Online Hallo is inrichting een handmatige taak.

**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**

1. Meld u bij tooyour **ArcGIS** tenant.

2. Klik op **leden UITNODIGEN**.
   
    ![Leden uitnodigen](./media/active-directory-saas-arcgis-tutorial/ic784747.png "leden uit te nodigen")

3. Selecteer **automatisch leden toevoegen zonder een e-mailbericht te verzenden**, en klik vervolgens op **volgende**.
   
    ![Automatisch toevoegen van leden](./media/active-directory-saas-arcgis-tutorial/ic784748.png "automatisch toevoegen van leden")

4. Op Hallo **leden** dialoogvenster pagina, voert u Hallo stappen te volgen:
   
     ![Toevoegen en controleren](./media/active-directory-saas-arcgis-tutorial/ic784749.png "toevoegen en controleren")
    
     a. Voer Hallo **e**, **voornaam**, en **achternaam** van een geldige AAD-account dat u wilt dat tooprovision.
  
     b. Klik op **toevoegen en bekijk**.
5. Bekijk Hallo gegevens die u hebt ingevoerd, en klik vervolgens op **leden toevoegen**.
   
    ![Lid toevoegen](./media/active-directory-saas-arcgis-tutorial/ic784750.png "lid toevoegen")
        
    > [!NOTE]
    > Hello Azure Active Directory-accounthouder wordt een e-mailbericht ontvangen en volg een koppeling tooconfirm hun account maken voordat deze geactiveerd wordt.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooArcGIS Online.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooArcGIS Online uitvoeren Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **ArcGIS Online**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Wanneer u Online ArcGIS Hallo-tegel in Hallo toegangsvenster klikt, krijgt u automatisch aangemelde tooyour ArcGIS on line toepassing.
Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_203.png

