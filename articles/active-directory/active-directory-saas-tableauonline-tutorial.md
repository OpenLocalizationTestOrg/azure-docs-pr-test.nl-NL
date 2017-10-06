---
title: 'Zelfstudie: Azure Active Directory-integratie met Tableau Online | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding van Azure Active Directory en Tableau Online.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d4b1149-ba3b-4f4e-8bce-9791316b730d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 590b2674270c340b4750c7b6feeaf4f0df4bf853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a>Zelfstudie: Azure Active Directory-integratie met Tableau Online

In deze zelfstudie leert u hoe toointegrate Tableau Online met Azure Active Directory (Azure AD).

Online Tableau integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die Online tooTableau toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooTableau Online (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Tableau Online tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Tableau Online eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Online Tableau van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-tableau-online-from-hello-gallery"></a>Het toevoegen van Online Tableau van Hallo-galerie
tooconfigure hello integratie Tableau online met Azure AD, moet u tooadd Tableau Online uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Tableau Online via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Tableau Online**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_search.png)

5. Selecteer in het deelvenster resultaten hello, **Tableau Online**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Tableau Online op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Tableau Online is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante Hallo-gebruiker in Tableau Online toobe tot stand gebracht.

In Online Tableau, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en test eenmalige aanmelding Azure AD met Tableau Online, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een Online Tableau testgebruiker](#creating-a-tableau-online-test-user)**  -toohave een equivalent van Britta Simon in Tableau Online die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Tableau Online configureren.

**Voer tooconfigure Azure AD eenmalige aanmelding met Online Tableau, Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Tableau Online** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_samlbase.png)

3. Op Hallo **Tableau Online domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_url.png)
    
    a. In Hallo **aanmeldings-URL** textbox type Hallo URL:`https://sso.online.tableau.com`

    b. In Hallo **id** textbox type Hallo URL:`https://sso.online.tableau.com/public/sp/<instancename>`

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/tutorial_general_400.png)

6. In een ander browservenster, aanmelding tooyour Tableau on line toepassing. Ga te**instellingen** en vervolgens **verificatie**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_09.png)
    
7. tooenable SAML onder **verificatietypen** sectie. Controleer de Hallo **eenmalige aanmelding met SAML** selectievakje.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_12.png)

8. Schuif omlaag totdat **metagegevensbestand importeren in Tableau Online** sectie.  Klik op Bladeren en importeer Hallo-metagegevensbestand die u hebt gedownload van Azure AD. Klik vervolgens op **toepassen**.
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_13.png)

9. In Hallo **overeen met asserties** sectie, plaatst u Hallo bijbehorende identiteitsprovider assertion naam voor **e-mailadres**, **voornaam**, en **achternaam** . tooget deze gegevens vanuit Azure AD: 
  
    a. In hello Azure-portal, gaat u op Hallo **Tableau Online** pagina van de integratie van toepassingen.
    
    b. Selecteer in de sectie kenmerken Hallo Hallo **'weergeven en bewerken van alle andere gebruikerskenmerken '** selectievakje. 
    
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/attributesection.png)
      
    c. Hallo namespace-waarde van deze kenmerken kopiëren: givenname, e-mail- en achternaam met behulp van Hallo volgende stappen:

   ![Azure AD voor eenmalige aanmelding](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_10.png)
    
    d. Klik op **user.givenname** waarde 
    
    e. Hallo-waarde in Hallo kopiëren **naamruimte** textbox.

   ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/attributesection2.png)

    f. toocopy hello namesapce waarden voor Hallo e-mail- en achternaam volgen Hallo vorige stappen.

    g. Schakel over naar toohello Tableau on line toepassing en stel vervolgens Hallo **Tableau Online kenmerken** sectie als volgt:
     * E-mailadres: **mail** of **userprincipalname**
     * Voornaam: **givenname**
     * Achternaam: **achternaam**
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_14.png)

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-tableau-online-test-user"></a>Maken van een Online Tableau testgebruiker

In deze sectie maakt maken u een gebruiker die is aangeroepen terwijl Britta Simon Tableau Online.

1. Op **Tableau Online**, klikt u op **instellingen** en vervolgens **verificatie** sectie. Schuif naar beneden te**gebruikers selecteren** sectie. Klik op **gebruikers toevoegen** en vervolgens **Voer e-mailadressen**.
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_15.png)
2. Selecteer **toevoegen van gebruikers voor eenmalige aanmelding (SSO) verificatie**. In Hallo **e-mailadressen opgeven** textbox toevoegenbritta.simon@contoso.com
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_11.png)
3. Klik op **Create**.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooTableau Online.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooTableau Online uitvoeren Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Tableau Online**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.

Wanneer u Online Tableau Hallo-tegel in Hallo toegangsvenster klikt, krijgt u automatisch aangemelde tooyour Tableau on line toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_203.png

