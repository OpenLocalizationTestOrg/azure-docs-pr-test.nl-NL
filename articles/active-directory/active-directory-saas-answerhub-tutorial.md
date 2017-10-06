---
title: 'Zelfstudie: Azure Active Directory-integratie met AnswerHub | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en AnswerHub.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 818b91d7-01df-4b36-9706-f167c710a73c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 90b530da31abe7e6f18bfa2c5409f8ff1d4f1063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-answerhub"></a>Zelfstudie: Azure Active Directory-integratie met AnswerHub

In deze zelfstudie leert u hoe toointegrate AnswerHub met Azure Active Directory (Azure AD).

AnswerHub integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooAnswerHub toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooAnswerHub (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met AnswerHub tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een AnswerHub eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van AnswerHub van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-answerhub-from-hello-gallery"></a>Het toevoegen van AnswerHub van Hallo-galerie
tooconfigure hello integratie van AnswerHub in Azure AD, moet u tooadd AnswerHub uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd AnswerHub via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **AnswerHub**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_search.png)

5. Selecteer in het deelvenster resultaten hello, **AnswerHub**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met AnswerHub op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in AnswerHub is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in AnswerHub toobe tot stand gebracht.

Wijs in AnswerHub, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met AnswerHub, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker AnswerHub](#creating-an-answerhub-test-user)**  -toohave een equivalent van Britta Simon in AnswerHub die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing AnswerHub configureren.

**Azure AD tooconfigure eenmalige aanmelding met AnswerHub, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **AnswerHub** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_samlbase.png)

3. Op Hallo **AnswerHub domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company>.answerhub.com`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<company>.answerhub.com`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id. Neem contact op met [AnswerHub Client ondersteuningsteam](mailto:success@answerhub.com) tooget deze waarden. 
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-answerhub-tutorial/tutorial_general_400.png)

6. Op Hallo **AnswerHub configuratie** sectie, klikt u op **configureren AnswerHub** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out URL's, en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_configure.png) 

7. In een ander browservenster, meld u bij uw bedrijf AnswerHub site als beheerder.
   
    >[!NOTE]
    >Als u nodig hebt bij het configureren van AnswerHub, neem dan contact op met [ondersteuningsteam van AnswerHub](mailto:success@answerhub.com.).
   
8. Ga te**beheer**.

9. Klik op Hallo **gebruikers en groepen** tabblad.

10. In het navigatiedeelvenster Hallo op Hallo linkerkant in Hallo **sociale instellingen** sectie, klikt u op **SAML Setup**.

11. Klik op **IDP Config** tabblad.

12. Op Hallo **IDP Config** tabblad, voert u Hallo stappen te volgen:

     ![Setup van SAML](./media/active-directory-saas-answerhub-tutorial/ic785172.png "SAML Setup")  
  
     a. In **IDP aanmeldings-URL** textbox plakken **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.
  
     b. In **IDP afmelding URL** textbox plakken **Sign-Out URL** waarde die u hebt gekopieerd vanuit Azure-portal.
     
     c. In **IDP-naamnotatie id** textbox Voer Hallo gebruiker id dezelfde waarde als de geselecteerde in Azure-portal op **gebruikerskenmerken** sectie.
  
     d. Klik op **sleutels en certificaten**.

13. Voer op Hallo sleutels en certificaten tabblad Hallo stappen te volgen:
    
     ![Sleutels en certificaten](./media/active-directory-saas-answerhub-tutorial/ic785173.png "sleutels en certificaten")  
 
     a. Open uw base-64 gecodeerde certificaat dat u hebt gedownload vanuit Azure-portal in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **IDP openbare sleutel (x 509-indeling)** textbox.
  
     b. Klik op **Opslaan**.

14. Op Hallo **IDP Config** tabblad **opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-answerhub-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-answerhub-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-answerhub-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-answerhub-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-an-answerhub-test-user"></a>Een testgebruiker AnswerHub maken

Azure AD tooenable gebruikers toolog in tooAnswerHub, ze in AnswerHub moeten worden ingericht.  
In geval van AnswerHub Hallo is inrichting een handmatige taak.

**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**

1. Meld u bij tooyour **AnswerHub** bedrijf site als administrator.

2. Ga te**beheer**.

3. Klik op Hallo **gebruikers en groepen** tabblad.

4. In het navigatiedeelvenster Hallo op Hallo linkerkant in Hallo **gebruikers beheren** sectie, klikt u op **maken of importeren gebruikers**.
   
   ![Gebruikers en groepen](./media/active-directory-saas-answerhub-tutorial/ic785175.png "gebruikers en groepen")

5. Type Hallo **e-mailadres**, **gebruikersnaam** en **wachtwoord** van een geldig Azure Active Directory-account die u wilt dat tooprovision in Hallo tekstvakken gerelateerd en klik vervolgens op  **Sla**.

>[!NOTE]
>U kunt andere AnswerHub gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door AnswerHub tooprovision AAD-gebruikersaccounts.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooAnswerHub toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooAnswerHub, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **AnswerHub**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo AnswerHub tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour AnswerHub toepassing.
Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_203.png

