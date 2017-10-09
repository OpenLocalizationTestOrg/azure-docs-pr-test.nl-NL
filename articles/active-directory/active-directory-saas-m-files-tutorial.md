---
title: 'Zelfstudie: Azure Active Directory-integratie met M-bestanden | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en M-bestanden.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4536fd49-3a65-4cff-9620-860904f726d0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: e1d268da53312b1d2c12e29d66b1a5b66d0cdcce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-m-files"></a>Zelfstudie: Azure Active Directory-integratie met M-bestanden

In deze zelfstudie leert u hoe toointegrate M-bestanden met Azure Active Directory (Azure AD).

M-bestanden worden geïntegreerd met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooM-bestanden heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooM-bestanden (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

tooconfigure Azure AD-integratie met M-bestanden, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een M bestanden eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. M-bestanden uit de galerie Hallo toe te voegen.
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-m-files-from-hello-gallery"></a>M-bestanden uit de galerie Hallo toe te voegen.
tooconfigure hello integratie van M-bestanden met Azure AD, moet u tooadd M-bestanden uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd M-bestanden uit de galerie hello, Voer Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **M bestanden**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_search.png)

5. Selecteer in het deelvenster resultaten hello, **M bestanden**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met M-bestanden op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in M-bestanden is tooa gebruiker in Azure AD. Er moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in M-bestanden met andere woorden, toobe tot stand gebracht.

In de M-bestanden, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en test eenmalige aanmelding Azure AD met M-bestanden, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker M bestanden](#creating-a-m-files-test-user)**  -toohave een equivalent van Britta Simon in M-bestanden die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing M-bestanden.

**Azure AD tooconfigure eenmalige aanmelding met M-bestanden uitvoeren Hallo stappen te volgen:**

1. In Azure-portal op Hallo Hallo **M bestanden** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_samlbase.png)

3. Op Hallo **M bestanden domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<tenantname>.cloudvault.m-files.com`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id. Neem contact op met [M bestanden Client ondersteuningsteam](mailto:support@m-files.com) tooget deze waarden. 
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-m-files-tutorial/tutorial_general_400.png)

6. tooget SSO geconfigureerd voor uw toepassing, neem contact op met [M bestanden ondersteuningsteam](mailto:support@m-files.com) en bieden ze Hallo metagegevens gedownload.
   
    >[!NOTE]
    >Voer Hallo volgende stappen uit als u wilt dat tooconfigure eenmalige aanmelding voor u bureaubladtoepassing M-bestand. Er zijn geen extra stappen vereist als u alleen tooconfigure eenmalige aanmelding voor de webversie M-bestanden.  

7. Ga als volgt Hallo volgende stappen tooconfigure Hallo M bestand bureaubladtoepassing tooenable eenmalige aanmelding met Azure AD. toodownload M-bestanden te gaan[M-bestanden downloaden](https://www.m-files.com/en/download-latest-version) pagina.

8. Open Hallo **M bestanden bureaublad instellingen** venster. Klik vervolgens op **toevoegen**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_10.png)

9. Op Hallo **Document kluis verbindingseigenschappen** venster Hallo volgende stappen uit te voeren:
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_11.png)  

    Hallo onder sectie servertype hello, als volgt waarden op:  

    a. Voor **naam**, type `<tenant-name>.cloudvault.m-files.com`. 
 
    b. Voor **poortnummer**, type **4466**. 

    c. Voor **Protocol**, selecteer **HTTPS**. 

    d. In Hallo **verificatie** optie **specifieke Windows-gebruiker**. Vervolgens wordt u gevraagd met een pagina ondertekenen. Voeg in uw Azure AD-referenties. 

    e. Voor Hallo **kluis op Server**, selecteer Hallo betreffende kluis op de server.
 
    f. Klik op **OK**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-m-files-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-m-files-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-m-files-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-m-files-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-m-files-test-user"></a>Een testgebruiker M-bestanden maken

Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in M-bestanden van een gebruiker. Werken met [M bestanden ondersteuningsteam](mailto:support@m-files.com) tooadd Hallo gebruikers in Hallo M-bestanden.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tot tooM-bestanden.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooM-bestanden, voert u Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **M bestanden**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.

Wanneer u klikt op Hallo M-bestanden in Hallo Toegangsvenster tegel, krijgt u de toepassing automatisch aangemelde tooyour M-bestanden.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_203.png

