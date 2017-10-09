---
title: 'Zelfstudie: Azure Active Directory-integratie met Five9 Plus Adapter (CTI, neem contact op met Center-Agents) | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Five9 Plus Adapter (CTI, neem contact op met Center-Agents).
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 88dc82ab-be0b-4017-8335-c47d00775d7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: 2e3ea8b5f2a6eaa8ad17d39e03fa490038b14561
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-five9-plus-adapter-cti-contact-center-agents"></a>Zelfstudie: Azure Active Directory-integratie met Five9 Plus Adapter (CTI, neem contact op met Center-Agents)

In deze zelfstudie leert u hoe toointegrate Five9 Plus Adapter (CTI, neem contact op met Center-Agents) met Azure Active Directory (Azure AD).

Five9 Plus Adapter (CTI, neem contact op met Center-Agents) integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie heeft toegang tot tooFive9 Plus Adapter (CTI, neem contact op met Center-Agents)
- U kunt uw gebruikers tooautomatically get aangemelde tooFive9 Plus Adapter (CTI, neem contact op met Center-Agents) inschakelen (Single Sign-On) met hun Azure AD-accounts
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

tooconfigure Azure AD-integratie met Five9 Plus Adapter (CTI, neem contact op met Center-Agents), moet u de volgende items Hallo:

- Een Azure AD-abonnement
- Een Five9 Plus Adapter (CTI, neem contact op met Center-Agents) eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Five9 Plus Adapter (CTI, neem contact op met Center-Agents) uit de galerie Hallo toevoegen
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-five9-plus-adapter-cti-contact-center-agents-from-hello-gallery"></a>Five9 Plus Adapter (CTI, neem contact op met Center-Agents) uit de galerie Hallo toevoegen
tooconfigure hello integratie van Five9 Plus Adapter (CTI, neem contact op met Center-Agents) in Azure AD, moet u tooadd Five9 Plus Adapter (CTI, neem contact op met Center-Agents) uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Five9 Plus Adapter (CTI, neem contact op met Center-Agents) uit de galerie hello, Voer Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Five9 Plus Adapter (CTI, neem contact op met Center-Agents)**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-five9-tutorial/tutorial_five9_search.png)

5. Selecteer in het deelvenster resultaten hello, **Five9 Plus Adapter (CTI, neem contact op met Center-Agents)**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-five9-tutorial/tutorial_five9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met Five9 Plus-Adapter (CTI, neem contact op met Center-Agents) op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent Five9 Plus adapter (CTI, neem contact op met Center-Agents) is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo Five9 Plus adapter (CTI, neem contact op met Center-Agents) toobe tot stand gebracht.

Five9 Plus adapter (CTI, neem contact op met Center-Agents), wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en test eenmalige aanmelding Azure AD met Five9 Plus Adapter (CTI, neem contact op met Center-Agents), moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Five9 Plus Adapter (CTI, neem contact op met Center-Agents)](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)**  -toohave een equivalent van Britta Simon Five9 Plus adapter (CTI, neem contact op met Center-Agents) die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Five9 Plus Adapter (CTI, neem contact op met Center-Agents).

**tooconfigure eenmalige aanmelding Azure AD met Five9 Plus Adapter (CTI, neem contact op met Center-Agents), Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Five9 Plus Adapter (CTI, neem contact op met Center-Agents)** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-five9-tutorial/tutorial_five9_samlbase.png)

3. Op Hallo **Five9 Plus Adapter (CTI, neem contact op met Center-Agents)-domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-five9-tutorial/tutorial_five9_url.png)
    
    a. In Hallo **id** textbox, type patronen u een URL met hello te volgen:

    |    Omgeving      |       URL      |
    | :-- | :-- |
    | Voor 'Five9 Plus Adapter voor Microsoft Dynamics CRM' | `https://app.five9.com/appsvcs/saml/metadata/alias/msdc` |
    | Voor 'Five9 Plus Adapter voor Zendesk' | `https://app.five9.com/appsvcs/saml/metadata/alias/zd` |
    | Voor 'Five9 Plus Adapter voor bureaublad Toolkit Agent' | `https://app.five9.com/appsvcs/saml/metadata/alias/adt` |

    b. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:

    |      Omgeving     |      URL      |
    | :--                  | :--           |
    | Voor 'Five9 Plus Adapter voor Microsoft Dynamics CRM' | `https://app.five9.com/appsvcs/saml/SSO/alias/msdc` |
    | Voor 'Five9 Plus Adapter voor Zendesk' | `https://app.five9.com/appsvcs/saml/SSO/alias/zd` |
    | Voor 'Five9 Plus Adapter voor bureaublad Toolkit Agent' | `https://app.five9.com/appsvcs/saml/SSO/alias/adt` |

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-five9-tutorial/tutorial_five9_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-five9-tutorial/tutorial_general_400.png)

6. Op Hallo **Five9 Plus (CTI, neem contact op met Center-Agents) adapterconfiguratie** sectie, klikt u op **configureren Five9 Plus Adapter (CTI, neem contact op met Center-Agents)** tooopen **aanmeldingconfigureren** venster. Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-five9-tutorial/tutorial_five9_configure.png) 

7. tooconfigure eenmalige aanmelding op **Five9 Plus Adapter (CTI, neem contact op met Center-Agents)** zijde, moet u toosend Hallo gedownload **Certificate(Base64), Sign-Out URL SAML entiteit-ID en SAML Single Sign-On Service-URL** te[Five9 Plus Adapter (CTI, neem contact op met Center-Agents) ondersteuningsteam](https://www.five9.com/about/contact). Ook daarnaast voor het configureren van SSO verdere Volg Hallo onderstaande stappen volgens toohello adapter:

    a. 'Five9 Plus Adapter voor bureaublad Toolkit Agent' Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)
    
    b. 'Five9 Plus Adapter voor Microsoft Dynamics CRM' Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)
    
    c. 'Five9 Plus Adapter voor Zendesk' Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)


> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-five9-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-five9-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-five9-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-five9-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-five9-plus-adapter-cti-contact-center-agents-test-user"></a>Maken van een testgebruiker Five9 Plus Adapter (CTI, neem contact op met Center-Agents)

In deze sectie maakt u een gebruiker met de naam van Britta Simon Five9 Plus adapter (CTI, neem contact op met Center-Agents). Werken met [Five9 Plus Adapter (CTI, neem contact op met Center-Agents) ondersteuningsteam](https://www.five9.com/about/contact) Hallo gebruikers toevoegen in Hallo Five9 Plus Adapter (CTI, neem contact op met Center-Agents) platform. Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooFive9 Plus Adapter (CTI, neem contact op met Center-Agents).

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooFive9 Plus Adapter (CTI, neem contact op met Center-Agents), Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Five9 Plus Adapter (CTI, neem contact op met Center-Agents)**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-five9-tutorial/tutorial_five9_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Five9 Plus Adapter (CTI, neem contact op met Center-Agents)-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Five9 Plus Adapter (CTI, neem contact op met Center-Agents)-toepassing.
Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-five9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-five9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-five9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-five9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-five9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-five9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-five9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-five9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-five9-tutorial/tutorial_general_203.png

