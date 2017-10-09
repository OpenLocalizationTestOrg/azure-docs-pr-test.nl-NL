---
title: 'Zelfstudie: Azure Active Directory-integratie met Trello | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Trello.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cd5ae365-9ed6-43a6-920b-f7814b993949
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: de2f2ba6a0e5545983c351f26f99d14f436618c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trello"></a>Zelfstudie: Azure Active Directory-integratie met Trello

In deze zelfstudie leert u hoe toointegrate Trello met Azure Active Directory (Azure AD).

Trello integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooTrello toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooTrello (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Trello tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Trello eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Trello van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-trello-from-hello-gallery"></a>Het toevoegen van Trello van Hallo-galerie
tooconfigure hello integratie van Trello in Azure AD, moet u tooadd Trello uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Trello via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Trello**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-trello-tutorial/tutorial_trello_search.png)

5. Selecteer in het deelvenster resultaten hello, **Trello**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-trello-tutorial/tutorial_trello_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met Trello op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Trello is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Trello toobe tot stand gebracht.

Wijs in Trello, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Trello, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Trello](#creating-a-trello-test-user)**  -toohave een equivalent van Britta Simon in Trello die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Trello configureren.

**Azure AD tooconfigure eenmalige aanmelding met Trello, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Trello** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-trello-tutorial/tutorial_trello_samlbase.png)

3. Op Hallo **Trello domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **IDP geïnitieerd modus**, Hallo volgende stappen uit te voeren:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-trello-tutorial/tutorial_trello_url.png)

    In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://trello.com/auth/saml/consume/<enterprise>`

4. Op Hallo **Trello domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **SP geïnitieerd modus**, Hallo volgende stappen uit te voeren:
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-trello-tutorial/tutorial_trello_url1.png)

    a. Klik op Hallo **weergeven geavanceerde instellingen voor URL**.

    b. In Hallo **aanmelding op URL** textbox, typ een URL met Hallo patroon volgen:`https://trello.com/auth/saml/consume/<enterprise>`

    >[!NOTE]
    >Krijgt u Hallo  **\<enterprise\>**  slug van Trello. Als u geen Hallo slug waarde, neem dan contact op met [Trello ondersteuningsteam](mailto:support@trello.com) tooget Hallo slug voor u enterprise.
    > 

5. Trello toepassing verwacht hello SAML asserties toocontain specifieke kenmerken. Configureer Hallo kenmerken voor deze toepassing te volgen. U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo **'Gebruikerskenmerken'** van de toepassing hello. Hallo volgende Schermafbeelding toont een voorbeeld voor deze.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-trello-tutorial/tutorial_trello_attribute.png)

6. Op Hallo **SAML-token kenmerken** dialoogvenster uitvoeren Hallo volgende stappen uit voor elke rij in Hallo tabel hieronder weergegeven:
 
    | Naam van kenmerk | De waarde van kenmerk |
    | --- | --- |
    | User.Email | User.mail |
    | User.FirstName | User.givenName |
    | User.LastName | User.surname |

    a. Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-trello-tutorial/tutorial_officespace_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-trello-tutorial/tutorial_officespace_05.png)

    b. In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij. 

    c. Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.
    
    d. Klik op **OK**. 
 
7. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-trello-tutorial/tutorial_trello_certificate.png) 

8. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-trello-tutorial/tutorial_general_400.png)

6. Op Hallo **Trello configuratie** sectie, klikt u op **configureren Trello** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-trello-tutorial/tutorial_trello_configure.png) 

9. tooget SSO is geconfigureerd voor uw toepassing gaat te[Trello SSO Ondernemingsconfiguratie](https://trello.com/sso-configuration) pagina toosend [Trello ondersteuningsteam](mailto:support@trello.com) hello **SAML Single Sign-On Service-URL** en Hallo koppelen **certificaat (Base64)**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-trello-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-trello-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-trello-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-trello-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-trello-test-user"></a>Een testgebruiker Trello maken

In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Trello maken. In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Trello maken. Trello ondersteuning biedt voor just-in-time-inrichting en een nieuw account is gemaakt Hallo eerste keer dat u zich aanmeldt vanuit Azure AD.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooTrello toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooTrello, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Trello**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-trello-tutorial/tutorial_trello_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.

Als u op Hallo Trello tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Trello toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-trello-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trello-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trello-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trello-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trello-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trello-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trello-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trello-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trello-tutorial/tutorial_general_203.png

