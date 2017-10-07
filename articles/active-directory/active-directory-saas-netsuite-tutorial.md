---
title: 'Zelfstudie: Azure Active Directory-integratie met Netsuite | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Netsuite.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7cf205d5bda5333872fb589e57f4779a8670b595
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a>Zelfstudie: Azure Active Directory-integratie met Netsuite

In deze zelfstudie leert u hoe toointegrate Netsuite met Azure Active Directory (Azure AD).

Netsuite integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooNetsuite toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooNetsuite (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Netsuite tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Netsuite eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Netsuite van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-netsuite-from-hello-gallery"></a>Het toevoegen van Netsuite van Hallo-galerie
tooconfigure hello integratie van Netsuite in Azure AD, moet u tooadd Netsuite uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Netsuite via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. Klik op **nieuwe toepassing** knop op Hallo Hallo dialoogvenster bovenaan.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Netsuite**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. Selecteer in het deelvenster resultaten hello, **Netsuite**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Netsuite op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Netsuite is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Netsuite toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Netsuite.

tooconfigure en eenmalige aanmelding Azure AD-test met Netsuite, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Netsuite](#creating-a-netsuite-test-user)**  -toohave een equivalent van Britta Simon in Netsuite die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Netsuite configureren.

**Azure AD tooconfigure eenmalige aanmelding met Netsuite, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Netsuite** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. Op Hallo **Netsuite domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen: `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs``https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`

    > [!NOTE] 
    > Deze waarde is geen echte waarde. Waarde van de update Hallo met Hallo werkelijke antwoord-URL. Neem contact op met [Netsuite ondersteuningsteam](http://www.netsuite.com/portal/services/support.shtml) tooget deze waarde.
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. Op Hallo **Netsuite configuratie** sectie, klikt u op **configureren Netsuite** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. Een nieuw tabblad openen in uw browser en meld u aan bij uw site van het bedrijf Netsuite als beheerder.

8. Klik in de werkbalk bovenaan Hallo Hallo pagina Hallo op **Setup**, klikt u vervolgens op **Installatiebeheer**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. Van Hallo **instellingstaken** selecteert **integratie**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. In Hallo **verificatie beheren** sectie, klikt u op **SAML Single Sign-on**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. Op Hallo **SAML Setup** pagina, voert u Hallo stappen te volgen:
   
    a. Kopiëren Hallo **SAML Single Sign-On Service-URL** waarde uit de **Naslaggids** sectie van **eenmalige aanmelding configureren** en plak deze in Hallo **id-Provider Aanmeldingspagina** veld Netsuite.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    b. Selecteer in de Netsuite, **primaire methode voor netwerkverificatie**.

    c. Voor het Hallo-veld met het label **SAMLV2 identiteit Provider metagegevens**, selecteer **IDP metagegevens-bestand uploaden**. Klik vervolgens op **Bladeren** tooupload Hallo bestand met metagegevens dat u hebt gedownload vanuit Azure-portal.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    d. Klik op **indienen**.

12. In Azure AD, klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** selectievakje en het kenmerk toevoegen.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. Voor Hallo **kenmerknaam** veld, typt u in `account`. Voor Hallo **kenmerkwaarde** veld, typt u in uw Netsuite account-ID. Deze waarde is constante en wijzigen met account. Instructies voor het toofind je account-ID zijn hieronder vermeld:

      ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    a. In Netsuite, klikt u op **Setup** in Hallo bovenste navigatiebalk menu.

    b. Klik onder Hallo **instellingstaken** sectie van Hallo linkernavigatievenster menu, selecteer Hallo **integratie** sectie en op **Web Services-voorkeuren**.

    c. Kopieer uw Netsuite Account-ID en plak deze in Hallo **kenmerkwaarde** veld in Azure AD.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. Voordat gebruikers eenmalige aanmelding in Netsuite uitvoeren kunnen, moeten worden ze eerst de juiste machtigingen Hallo in Netsuite toegewezen. Volg onderstaande tooassign Hallo instructies deze machtigingen.

    a. Klik op het menu van de bovenste navigatiebalk hello, **Setup**, klikt u vervolgens op **Installatiebeheer**.
      
      ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    b. Selecteer Hallo linkernavigatievenster menu **gebruikers/rollen**, klikt u vervolgens op **rollen beheren**.
      
      ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    c. Klik op **nieuwe rol**.

    d. Typ in een **naam** voor uw nieuwe rol en selecteer Hallo **eenmalige aanmelding alleen** selectievakje.
      
      ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    e. Klik op **Opslaan**.

    f. Klik in het menu bovenaan Hallo Hallo **machtigingen**. Klik vervolgens op **Setup**.
      
       ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    g. Selecteer **ingesteld Up SAM Single Sign-on**, en klik vervolgens op **toevoegen**.

    h. Klik op **Opslaan**.

    ik. Klik op het menu van de bovenste navigatiebalk hello, **Setup**, klikt u vervolgens op **Installatiebeheer**.
      
       ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    j. Selecteer Hallo linkernavigatievenster menu **gebruikers/rollen**, klikt u vervolgens op **gebruikers beheren**.
      
       ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    k. Selecteer een testgebruiker. Klik vervolgens op **bewerken**.
      
       ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    l. Selecteer in het dialoogvenster Hallo rollen, Hallo-rol die u hebt gemaakt en klik op **toevoegen**.
      
       ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    m. Klik op **Opslaan**.
    
> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. Bovenaan Hallo Hallo dialoogvenster, klikt u op **toevoegen** tooopen hello **gebruiker** dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**. 

### <a name="creating-a-netsuite-test-user"></a>Een testgebruiker Netsuite maken

In deze sectie wordt een gebruiker met de naam Britta Simon gemaakt in Netsuite. Netsuite ondersteunt just-in-time-inrichting, die standaard is ingeschakeld.
Er is geen actie-item voor u in deze sectie. Als een gebruiker in Netsuite nog niet bestaat, wordt een nieuw gemaakt wanneer u tooaccess Netsuite probeert.


### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooNetsuite toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooNetsuite, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Netsuite**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

tootest uw eenmalige aanmelding-instellingen, open Hallo Toegangsvenster op [https://myapps.microsoft.com](https://myapps.microsoft.com/), meld u aan bij de testaccount Hallo en klikt u op **Netsuite**.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Gebruikers inrichten configureren](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png

