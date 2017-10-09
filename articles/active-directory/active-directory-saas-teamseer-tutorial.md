---
title: 'Zelfstudie: Azure Active Directory-integratie met TeamSeer | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en TeamSeer.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6ec4806f-fe0f-4ed7-8cfa-32d1c840433f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 876d13e446115acd50b01c7f44db99357045e429
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamseer"></a>Zelfstudie: Azure Active Directory-integratie met TeamSeer

In deze zelfstudie leert u hoe toointegrate TeamSeer met Azure Active Directory (Azure AD).

TeamSeer integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooTeamSeer toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooTeamSeer (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met TeamSeer tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een TeamSeer eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van TeamSeer van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-teamseer-from-hello-gallery"></a>Het toevoegen van TeamSeer van Hallo-galerie
tooconfigure hello integratie van TeamSeer in tooAzure AD, moet u tooadd TeamSeer uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd TeamSeer via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **TeamSeer**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_search.png)

5. Selecteer in het deelvenster resultaten hello, **TeamSeer**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met TeamSeer op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in TeamSeer is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in TeamSeer toobe tot stand gebracht.

Wijs in TeamSeer, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met TeamSeer, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker TeamSeer](#creating-a-teamseer-test-user)**  -toohave een equivalent van Britta Simon in TeamSeer die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing TeamSeer configureren.

**Azure AD tooconfigure eenmalige aanmelding met TeamSeer, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **TeamSeer** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_samlbase.png)

3. Op Hallo **TeamSeer domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_url.png)

     In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://www.teamseer.com/<companyid>`

    > [!NOTE] 
    > Hallo-waarde is geen echte. Waarde van de update Hallo met Hallo werkelijke aanmeldings-URL. Neem contact op met [TeamSeer Client ondersteuningsteam](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) tooget Hallo waarde. 
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamseer-tutorial/tutorial_general_400.png)

6. Op Hallo **TeamSeer configuratie** sectie, klikt u op **configureren TeamSeer** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_configure.png)

7. In een ander browservenster, meld u aan tooyour TeamSeer bedrijf site als een beheerder.

8. Ga te**HR Admin**.
   
    ![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789634.png "HR-beheerder")

9. Klik op **Setup**.
   
    ![Setup](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Setup")

10. Klik op **SAML provider details instellen**.
   
    ![Instellingen voor SAML](./media/active-directory-saas-teamseer-tutorial/ic789636.png "SAML-instellingen")

11. Voer in Hallo gedeelte details van SAML-provider, Hallo stappen te volgen:
   
    ![Instellingen voor SAML](./media/active-directory-saas-teamseer-tutorial/ic789637.png "SAML-instellingen")   

    a. Plakken Hallo **Single Sign-On Service-URL** waarde in toohello **URL** textbox.
          
    b. Open uw base-64 gecodeerde certificaat in Kladblok, kopie Hallo inhoud ervan in tooyour Klembord en plak deze toohello **IdP openbaar certificaat** textbox.

12. toocomplete hello SAML-configuratie van provider, voert u Hallo stappen te volgen:
    
    ![Instellingen voor SAML](./media/active-directory-saas-teamseer-tutorial/ic789638.png "SAML-instellingen") 

    a. In Hallo **e-mailadressen testen**, typ de e-mailadres Hallo test van de gebruiker. 
  
    b. In Hallo **verlener** textbox type Hallo URL-verlener van Hallo-provider. 
  
    c. Klik op **Opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamseer-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamseer-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamseer-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamseer-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-teamseer-test-user"></a>Een testgebruiker TeamSeer maken

Azure AD tooenable gebruikers toolog in tooTeamSeer, ze in tooShiftPlanning moeten worden ingericht. In geval van TeamSeer Hallo is inrichting een handmatige taak.

**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**

1. Meld u bij tooyour **TeamSeer** bedrijf site als beheerder.

2. Voer Hallo stappen te volgen:
   
    ![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789640.png "HR-beheerder")  
 
    a. Ga te**HR Admin \> gebruikers**.
  
    b. Klik op **uitvoeren van de wizard nieuwe gebruiker Hallo**.

3. In Hallo **Gebruikersdetails** sectie, voert u Hallo stappen te volgen:
   
    ![Details van gebruiker](./media/active-directory-saas-teamseer-tutorial/ic789641.png "Gebruikersdetails")

    a. Type Hallo **voornaam**, **achternaam**, **gebruikersnaam (e-mailadres)** van een geldige AAD-account dat u wilt dat tooprovision in toohello gerelateerde tekstvakken.
  
    b. Klik op **Volgende**.

4. Volg Hallo op het scherm instructies voor het toevoegen van een nieuwe gebruiker en klik op **voltooien**.

>[!NOTE]
>U kunt andere TeamSeer gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door TeamSeer tooprovision Azure AD-gebruikersaccounts. 

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooTeamSeer toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooTeamSeer, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **TeamSeer**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

Als u uw instellingen voor eenmalige aanmelding tootest wilt, open Hallo Toegangsvenster. Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_203.png

