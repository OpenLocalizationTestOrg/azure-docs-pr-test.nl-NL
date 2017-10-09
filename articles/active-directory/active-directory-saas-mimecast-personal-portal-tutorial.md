---
title: 'Zelfstudie: Azure Active Directory-integratie met de persoonlijke Portal Mimecast | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en persoonlijke Mimecast-Portal.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 345b22be-d87e-45a4-b4c0-70a67eaf9bfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: ee2a8edcab36f295732ac1ebe641ed7fcfc1f2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-personal-portal"></a>Zelfstudie: Azure Active Directory-integratie met Mimecast persoonlijke Portal

In deze zelfstudie leert u hoe toointegrate Mimecast persoonlijke Portal met Azure Active Directory (Azure AD).

Mimecast persoonlijke Portal integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooMimecast persoonlijke Portal heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooMimecast persoonlijke Portal (Single Sign-On) inschakelen met hun Azure AD-accounts
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met de persoonlijke Portal Mimecast tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een persoonlijke Portal Mimecast eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van persoonlijke Portal Mimecast van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-mimecast-personal-portal-from-hello-gallery"></a>Het toevoegen van persoonlijke Portal Mimecast van Hallo-galerie
tooconfigure hello integratie van persoonlijke Portal Mimecast in Azure AD, moet u tooadd Mimecast persoonlijke Portal uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Mimecast persoonlijke Portal via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Mimecast persoonlijke Portal**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_search.png)

5. Selecteer in het deelvenster resultaten hello, **Mimecast persoonlijke Portal**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Mimecast persoonlijke Portal op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Mimecast persoonlijke Portal is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Mimecast persoonlijke Portal toobe tot stand gebracht.

In Mimecast persoonlijke Portal Hallo waarde Hallo toewijzen **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en test eenmalige aanmelding Azure AD met Mimecast persoonlijke Portal, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Mimecast persoonlijke Portal](#creating-a-mimecast-personal-portal-test-user)**  -toohave een equivalent van Britta Simon in Mimecast persoonlijke Portal die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Mimecast persoonlijke Portal configureren.

**tooconfigure eenmalige aanmelding Azure AD met Mimecast persoonlijke Portal, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Mimecast persoonlijke Portal** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_samlbase.png)

3. Op Hallo **Mimecast persoonlijke Portal domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen: 
    | |     
    | ----------------------------------------|
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|
    | |
   
    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:

    | |     
    | --- |
    | `https://webmail-us.mimecast.com/sso/<companyname>`|
    | `https://webmail-uk.mimecast.com/sso/<companyname>`|    
    | `https://webmail-za.mimecast.com/sso/<companyname>`|
    | `https://webmail.mimecast-offshore.com/sso/<companyname>`|
    ||                                                 
    
    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id. Neem contact op met [Mimecast persoonlijke Portal Client ondersteuningsteam](https://www.mimecast.com/customer-success/technical-support/) tooget deze waarden. 
 


4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_400.png)

6. Op Hallo **Mimecast persoonlijke Portal-configuratie** sectie, klikt u op **Mimecast persoonlijke Portal configureren** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_configure.png) 

7. In een ander browservenster, meld u bij uw persoonlijke Mimecast-Portal als beheerder.

8. Ga te**Services \> toepassingen**.
   
    ![Toepassingen](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "toepassingen")

9. Klik op **verificatie profielen**.
   
    ![Verificatie profielen](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "verificatie-profielen")

10. Klik op **nieuwe Authentication profiel**.
   
    ![Nieuwe Authentication profiel](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "nieuwe profiel voor verificatie")

11. In Hallo **Authentication profiel** sectie, voert u Hallo stappen te volgen:
   
    ![Authentication profiel](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Authentication profiel")
   
    a. In Hallo **beschrijving** textbox, typ een naam voor uw configuratie.
   
    b. Selecteer **afdwingen van SAML-verificatie voor Mimecast Personal Portal**.
   
    c. Als **Provider**, selecteer **Azure Active Directory**.
   
    d. In **URL-verlener** textbox plakken Hallo-waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.
   
    e. In **aanmeldings-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.
   
    f. In **afmelding URL** textbox plakken Hallo-waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.

    g. Open uw **base 64-** gecodeerd certificaat in Kladblok gedownload vanuit Azure-portal kopie Hallo inhoud ervan naar het Klembord en plak deze toohello **Provider identiteitscertificaat (metagegevens)** tekstvak.

    h. Selecteer **toestaan voor eenmalige op**.
   
    ik. Klik op **Opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-mimecast-personal-portal-test-user"></a>Een testgebruiker Mimecast persoonlijke Portal maken

In volgorde tooenable Azure AD gebruikers toolog bij Mimecast persoonlijke Portal, moeten ze worden ingericht bij Mimecast persoonlijke Portal. In geval van persoonlijke Portal Mimecast Hallo is inrichting een handmatige taak.

Tooregister een domein moet u voordat u gebruikers kunt maken.

**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:**

1. Meld u aan bij tooyour **Mimecast persoonlijke Portal** als administrator.

2. Ga te**mappen \> intern**.
   
    ![Mappen](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "mappen")

3. Klik op **nieuwe domein registreren**.
   
    ![Nieuwe domein registreren](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "nieuwe domein registreren")

4. Nadat het nieuwe domein is gemaakt, klikt u op **nieuw adres**.
   
    ![Nieuw adres](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "nieuw adres")

5. Uitvoeren in het nieuwe adres dialoogvenster Hallo Hallo stappen uit te voeren van een geldig Azure AD-account die u wilt dat tooprovision:
   
    ![Sla](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "opslaan")
   
    a. In Hallo **e-mailadres** textbox type **e-mailadres** van Hallo gebruiker als  **BrittaSimon@contoso.com** .
    
    b. In Hallo **globale naam** textbox type Hallo **gebruikersnaam** als **BrittaSimon**.

    c. In Hallo **wachtwoord**, en **wachtwoord bevestigen** tekstvakken, type Hallo **wachtwoord** van Hallo-gebruiker.
   
    b. Klik op **Opslaan**.

>[!NOTE]
>U kunt geen andere hulpprogramma's voor persoonlijke Portal Mimecast gebruiker-account maken of API's die worden geleverd door Mimecast persoonlijke Portal tooprovision Azure AD-gebruikersaccounts gebruiken. 

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooMimecast persoonlijke Portal.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooMimecast persoonlijke Portal uitvoeren Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Mimecast persoonlijke Portal**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding
In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Mimecast persoonlijke Portal-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Mimecast persoonlijke Portal-toepassing. Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_203.png

