---
title: 'Zelfstudie: Azure Active Directory-integratie met BetterWorks | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en BetterWorks.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5bb9505a-be02-46ae-9979-5308715d2b47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 9803593124318ea82e5a8888cc5a95b5da84472e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-betterworks"></a>Zelfstudie: Azure Active Directory-integratie met BetterWorks

In deze zelfstudie leert u hoe toointegrate BetterWorks met Azure Active Directory (Azure AD).

BetterWorks integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooBetterWorks toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooBetterWorks (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met BetterWorks tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een BetterWorks eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van BetterWorks van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-betterworks-from-hello-gallery"></a>Het toevoegen van BetterWorks van Hallo-galerie
tooconfigure hello integratie van BetterWorks in Azure AD, moet u tooadd BetterWorks uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd BetterWorks via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **BetterWorks**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_search.png)

5. Selecteer in het deelvenster resultaten hello, **BetterWorks**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met BetterWorks op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in BetterWorks is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in BetterWorks toobe tot stand gebracht.

Wijs in BetterWorks, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met BetterWorks, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker BetterWorks](#creating-a-betterworks-test-user)**  -toohave een equivalent van Britta Simon in BetterWorks die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing BetterWorks configureren.

**Azure AD tooconfigure eenmalige aanmelding met BetterWorks, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **BetterWorks** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_samlbase.png)

3. Op Hallo **BetterWorks domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **IDP geïnitieerd modus**:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url.png)

    a. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://app.betterworks.com/saml2/metadata/`

    b. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://app.betterworks.com/saml2/acs/`

4. Op Hallo **BetterWorks domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **SP geïnitieerd modus**, Hallo volgende stappen uit te voeren:
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url1.png)

    a. Klik op Hallo **weergeven geavanceerde instellingen voor URL**.

    b. In Hallo **aanmelding op URL** textbox, typ een URL met Hallo patroon volgen:`https://app.betterworks.com`

    > [!NOTE] 
    > Deze zijn niet echte waarden. Deze waarden Hello antwoord-URL-id en de werkelijke aanmelding op URL bijwerken. Neem contact op met [BetterWorks ondersteuningsteam](mailto:support@betterworks.com) tooget deze waarden.
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_certificate.png)  

5. Hallo SAML asserties verwacht BetterWorks toepassing in een specifieke indeling. Configureer Hallo claims voor deze toepassing te volgen. U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo '**kenmerk**' tabblad van de toepassing hello. Hallo volgende Schermafbeelding toont een voorbeeld voor deze. 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_attribute.png)

6. Op Hallo **SAML-token kenmerken** dialoogvenster uitvoeren Hallo volgende stappen uit voor elke rij in Hallo tabel hieronder weergegeven:
 
   | Naam van kenmerk | De waarde van kenmerk |
   | -------------- |  ------------ |
   | saml_token     | bd189cf6-1701-11e6-8f90-d26992eca2a5 |

   a. Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_05.png)

   b. In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij. 

   c. Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.
    
   d. Klik op **OK**.

7. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-betterworks-tutorial/tutorial_general_400.png)

8. tooconfigure eenmalige aanmelding op **BetterWorks** zijde, moet u toosend Hallo gedownload **Metadata XML** te[BetterWorks ondersteuningsteam](mailto:support@betterworks.com).


> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-betterworks-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-betterworks-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-betterworks-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-betterworks-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-betterworks-test-user"></a>Een testgebruiker BetterWorks maken

In deze sectie kunt u een gebruiker Britta Simon aangeroepen in BetterWorks maken. Werken met [BetterWorks ondersteuningsteam](mailto:support@betterworks.com) tooadd Hallo gebruikers in Hallo BetterWorks platform.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooBetterWorks toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooBetterWorks, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **BetterWorks**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.

Als u op Hallo BetterWorks-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour BetterWorks toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_203.png

