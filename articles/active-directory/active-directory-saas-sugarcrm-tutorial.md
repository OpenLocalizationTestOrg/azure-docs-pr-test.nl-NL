---
title: 'Zelfstudie: Azure Active Directory-integratie met suiker CRM | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en suiker CRM.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3331b9fc-ebc0-4a3a-9f7b-bf20ee35d180
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 108d2f8125e410743ee7bc48883a1d0b00602615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sugar-crm"></a>Zelfstudie: Azure Active Directory-integratie met suiker CRM

In deze zelfstudie leert u hoe toointegrate suiker CRM met Azure Active Directory (Azure AD).

Suiker CRM integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooSugar CRM heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooSugar CRM (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met suiker CRM tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een CRM suiker eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van suiker CRM van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-sugar-crm-from-hello-gallery"></a>Het toevoegen van suiker CRM van Hallo-galerie
tooconfigure hello integratie van suiker CRM in Azure AD, moet u tooadd suiker CRM uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd suiker CRM via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **suiker CRM**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_search.png)

5. Selecteer in het deelvenster resultaten hello, **suiker CRM**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met suiker CRM op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in suiker CRM is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in suiker CRM toobe tot stand gebracht.

In suiker CRM, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en test eenmalige aanmelding Azure AD met suiker CRM, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker suiker CRM](#creating-a-sugar-crm-test-user)**  -toohave een equivalent van Britta Simon in suiker CRM die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing suiker CRM.

**Azure AD tooconfigure eenmalige aanmelding met suiker CRM, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **suiker CRM** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_samlbase.png)

3. Op Hallo **suiker CRM-domein en URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_url.png)

    In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:
    | |
    |--|
    | `https://<companyname>.sugarondemand.com` |
    | `https://<companyname>.trial.sugarcrm` |

    > [!NOTE] 
    > Hallo-waarde is geen echte. Waarde van de update Hallo met Hallo werkelijke aanmeldings-URL. Neem contact op met [suiker CRM-Client-ondersteuningsteam](https://support.sugarcrm.com/) tooget Hallo waarde. 
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_400.png)

6. Op Hallo **suiker CRM configuratie** sectie, klikt u op **configureren suiker CRM** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out URL's, en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_configure.png) 

7. In een ander browservenster, meld u aan tooyour suiker CRM bedrijf site als een beheerder.

8. Ga te**Admin**.
   
    ![Beheerder](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")

9. In Hallo **beheer** sectie, klikt u op **wachtwoordbeheer**.
   
    ![Beheer](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "beheer")

10. Selecteer **SAML-verificatie inschakelen**.
   
    ![Beheer](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "beheer")

11. In Hallo **SAML-verificatie** sectie, voert u Hallo stappen te volgen:
   
    ![SAML-verificatie](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "SAML-verificatie")  
 
    a. In Hallo **aanmeldings-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.
  
    b. In Hallo **SLO URL** textbox plakken Hallo-waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.
  
    c. De base-64 gecodeerde certificaat openen in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak Hallo gehele certificaat in **X.509-certificaat** textbox.
  
    d. Klik op **Opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-sugar-crm-test-user"></a>Een testgebruiker suiker CRM maken

In de volgorde tooenable Azure AD gebruikers toolog in tooSugar CRM, moeten ze ingerichte tooSugar CRM zijn.

In geval van suiker CRM Hallo is inrichting een handmatige taak.

**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**

1. Meld u bij tooyour **suiker CRM** bedrijf site als administrator.

2. Ga te**Admin**.
   
    ![Beheerder](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")

3. In Hallo **beheer** sectie, klikt u op **Gebruikersbeheer**.
   
    ![Beheer](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "beheer")

4. Ga te**gebruikers \> nieuwe gebruiker maken**.
   
    ![Nieuwe gebruiker maken](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "nieuwe gebruiker maken")

5. Op Hallo **gebruikersprofiel** tabblad, voert u Hallo stappen te volgen:
   
    ![Nieuwe gebruiker](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "nieuwe gebruiker")

    a. Type Hallo **gebruikersnaam**, **achternaam**, en **e-mailadres** van een geldige Azure Active Directory-gebruiker in Hallo gerelateerde tekstvakken.
  
6. Als **Status**, selecteer **Active**.

7. Op tabblad hello, voert u Hallo stappen te volgen:
   
    ![Nieuwe gebruiker](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "nieuwe gebruiker")

    a. Geef het wachtwoord Hallo in Hallo gerelateerd textbox.

    b. Klik op **Opslaan**.

>[!NOTE]
>U kunt andere suiker CRM gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door suiker CRM tooprovision AAD-gebruikersaccounts. 
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooSugar CRM.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooSugar CRM, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **suiker CRM**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.

Als u op Hallo suiker CRM-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour suiker CRM-toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_203.png

