---
title: 'Zelfstudie: Azure Active Directory-integratie met Marketo | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Marketo.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 87f88cde4f027f99a83c1ab3b318247bb4d658ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a>Zelfstudie: Azure Active Directory-integratie met Marketo

In deze zelfstudie leert u hoe toointegrate Marketo met Azure Active Directory (Azure AD).

Marketo integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooMarketo toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooMarketo (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Marketo tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Marketo-eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Marketo van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-marketo-from-hello-gallery"></a>Het toevoegen van Marketo van Hallo-galerie
tooconfigure hello integratie van Marketo in Azure AD, moet u tooadd Marketo uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Marketo via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Marketo**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_search.png)

5. Selecteer in het deelvenster resultaten hello, **Marketo**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Marketo op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Marketo is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Marketo toobe tot stand gebracht.

Wijs in Marketo Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Marketo, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Marketo](#creating-a-marketo-test-user)**  -toohave een equivalent van Britta Simon in Marketo die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Marketo.

**Voer tooconfigure Azure AD eenmalige aanmelding met Marketo Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Marketo** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_samlbase.png)

3. Op Hallo **Marketo-domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_url.png)

    a. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://saml.marketo.com/sp`

    b. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://login.marketo.com/saml/assertion/\<munchkinid\>`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Werk deze waarden met Hallo werkelijke id en de antwoord-URL. Neem contact op met [Marketo-ondersteuningsteam](http://investors.marketo.com/contactus.cfm) tooget deze waarden.
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_general_400.png)

6. Op Hallo **Marketo configuratie** sectie, klikt u op **configureren Marketo** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_configure.png) 

7. tooget Munchkin-Id van uw toepassing met behulp van beheerdersreferenties tooMarketo aanmelden en volgende acties uitvoeren:
   
    a. Meld u aan met beheerdersreferenties tooMarketo-app.
   
    b. Klik op Hallo **Admin** knop op Hallo bovenste navigatiedeelvenster.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    c. Toohello integratie menu Navigeren en klik op Hallo **Munchkin koppeling**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_11.png)
   
    d. Kopieer Hallo weergegeven op het welkomstscherm Munchkin-Id en uw antwoord-URL in de configuratiewizard hello Azure AD te voltooien.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_12.png) 

8. tooconfigure hello eenmalige aanmelding in de toepassing hello, volg Hallo onderstaande stappen te volgen:
   
    a. Meld u aan met beheerdersreferenties tooMarketo-app.
   
    b. Klik op Hallo **Admin** knop op Hallo bovenste navigatiedeelvenster.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    c. Navigeer toohello integratie menu en klik op **eenmalige aanmelding**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_07.png) 
   
    d. tooenable hello SAML-instellingen, klikt u op **bewerken** knop.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_08.png) 
   
    e. **Ingeschakeld** Single Sign-On-instellingen.
   
    f. Plakken Hallo **SAML entiteit-ID**, in Hallo **uitgever-ID** textbox.
   
    g. In Hallo **entiteit-ID** textbox Voer Hallo-URL als `http://saml.marketo.com/sp`.
   
    h. Selecteer Hallo locatie van de ID van de gebruiker als **naam-ID-element**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > Als uw gebruikers-id geen UPN-naam en waarde voor het Hallo Hallo kenmerk tabblad wijzigen is.
   
    ik. Hallo-certificaat dat u hebt gedownload van Azure AD-configuratiewizard uploaden. **Sla** Hallo instellingen.
   
    j. Hallo omleidingspagina's instellingen bewerken.
   
    k. Plakken Hallo **SAML Single Sign-On Service-URL** in Hallo **aanmeldings-URL** textbox.
   
    l. Plakken Hallo **Sign-Out URL** in Hallo **afmelding URL** textbox.
   
    m. In Hallo **Error URL**, kopie uw **Marketo exemplaar-URL** en klik op **opslaan** knop toosave instellingen.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_10.png)

9. tooenable hello eenmalige aanmelding voor gebruikers, volledige Hallo van de volgende activiteiten:
   
    a. Meld u aan met beheerdersreferenties tooMarketo-app.
   
    b. Klik op Hallo **Admin** knop op Hallo bovenste navigatiedeelvenster.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    c. Navigeer toohello **beveiliging** en klik op **aanmeldingsinstellingen**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_13.png)
   
    d. Controleer Hallo **vereisen SSO** optie en **opslaan** Hallo instellingen.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-marketo-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-marketo-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-marketo-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-marketo-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-marketo-test-user"></a>Een testgebruiker Marketo maken

In deze sectie maakt maken u een gebruiker Britta Simon aangeroepen in Marketo. Volg deze stappen toocreate een gebruiker in Marketo-platform.

1. Meld u aan met beheerdersreferenties tooMarketo-app.

2. Klik op Hallo **Admin** knop op Hallo bovenste navigatiedeelvenster.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 

3. Navigeer toohello **beveiliging** en klik op **gebruikers en rollen**
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_19.png)  

4. Klik op Hallo **nieuwe gebruikers uitnodigen** koppeling op een tabblad Hallo-gebruikers
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_15.png) 

5. In Hallo nieuwe gebruikers uitnodigen wizard opvulling Hallo volgende informatie
   
    a. Voer Hallo gebruiker **e** adres in het tekstvak Hallo
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_16.png)
   
    b. Voer Hallo **voornaam** in Hallo tekstvak
   
    c. Voer Hallo **achternaam** in Hallo tekstvak
   
    d. Klik op **Volgende**

6. In Hallo **machtigingen** tabblad, selecteer Hallo **userRoles** en klik op **volgende**
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_17.png)
7. Klik op Hallo **verzenden** knop toosend Hallo gebruiker uitnodiging
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_18.png)

8. Gebruiker Hallo e-mailmelding ontvangt en tooclick Hallo koppelen en Hallo wachtwoord tooactivate Hallo account wijzigen. 

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooMarketo toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooMarketo, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Marketo**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Marketo-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Marketo-toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_203.png

