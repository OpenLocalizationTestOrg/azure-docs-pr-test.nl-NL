---
title: 'Zelfstudie: Azure Active Directory-integratie met SAP Business Object Cloud | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en SAP Business Object Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 6c5e44f0-4e52-463f-b879-834d80a55cdf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: a3e9bd93897271531f91bcbc50cd361e8a20551e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-object-cloud"></a>Zelfstudie: Azure Active Directory-integratie met SAP Business Object Cloud

In deze zelfstudie leert u hoe toointegrate SAP Business Object Cloud met Azure Active Directory (Azure AD).

U de volgende voordelen wanneer u een SAP Business Object Cloud met Azure AD integreert Hallo krijgen:

- In Azure AD, kunt u bepalen wie toegang tooSAP Business Object Cloud heeft.
- U kunt uw gebruikers tooSAP Business Object Cloud automatisch aanmelden met behulp van eenmalige aanmelding en Azure AD-account van een gebruiker.
- U kunt uw accounts op één centrale locatie hello Azure-portal beheren.

Zie toolearn meer informatie over de software als een dienst (SaaS)-app-integratie met Azure AD [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

tooset van Azure AD-integratie met SAP Business Object Cloud, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een SAP Business Object Cloud met eenmalige aanmelding ingeschakeld

> [!NOTE]
> Als u Hallo stappen in deze zelfstudie hebt getest, wordt u aangeraden dat u deze niet in een productieomgeving testen.

Aanbevelingen voor het testen van Hallo stappen in deze zelfstudie:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een gratis proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. 

Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. SAP Business Object Cloud uit de galerie Hallo toevoegen.
2. Instellen en testen van eenmalige aanmelding Azure AD.

## <a name="add-sap-business-object-cloud-from-hello-gallery"></a>SAP Business Object Cloud van Hallo galerie toevoegen
tooset van integratie van SAP Business Object Cloud met Azure AD in de galerie Hallo Hallo SAP Business Object Cloud tooyour lijst met beheerde SaaS-apps toevoegen.

tooadd SAP Business Object Cloud uit de galerie Hallo:

1. In Hallo [Azure-portal](https://portal.azure.com), Hallo linkermenu in, selecteer **Azure Active Directory**. 

    ![Hello Azure Active Directory-knop][1]

2. Selecteer **bedrijfstoepassingen**, en selecteer vervolgens **alle toepassingen**.

    ![pagina met toepassingen Hallo Enterprise][2]
    
3. Selecteer een nieuwe toepassing tooadd **nieuwe toepassing**.

    ![knop voor nieuwe toepassing Hello][3]

4. Voer in het zoekvak Hallo **SAP Business Object Cloud**.

    ![Hallo zoekvak](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_search.png)

5. Selecteer in het deelvenster resultaten hello, **SAP Business Object Cloud**, en selecteer vervolgens **toevoegen**.

    ![SAP Business Object Cloud in de lijst met resultaten Hallo](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_addfromgallery.png)

##  <a name="set-up-and-test-azure-ad-single-sign-on"></a>Instellen en testen eenmalige aanmelding Azure AD

In deze sectie kunt u instellen en eenmalige aanmelding Azure AD-test met SAP Business Object Cloud op basis van een testgebruiker met de naam *Britta Simon*.

Voor één aanmelding toowork moet Azure AD tooknow hello Azure AD-equivalent gebruiker in de Cloud voor SAP Business-Object. Een koppeling relatie tussen een Azure AD-gebruiker en de verwante Hallo-gebruiker in een SAP Business Object Cloud moet worden ingesteld.

Hallo tooestablish relatie in SAP Business Object Cloud koppelen voor **gebruikersnaam**, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD.

tooconfigure en eenmalige aanmelding Azure AD-test met SAP Business Object Cloud, volledige Hallo taken te volgen:

1. [Instellen van eenmalige aanmelding Azure AD](#set-up-azure-ad-single-sign-on). Een gebruiker toouse ingesteld met deze functie.
2. [Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user). Azure AD tests eenmalige aanmelding met Hallo gebruiker Britta Simon.
3. [Maken van een SAP Business Object Cloud testgebruiker](#create-an-sap-business-object-cloud-test-user). Maakt een equivalent van Britta Simon in SAP Business Object Cloud die is gekoppeld toohello Azure AD-weergave van Hallo gebruiker.
4. [Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user). Stelt Britta Simon toouse eenmalige aanmelding Azure AD.
5. [Test eenmalige aanmelding](#test-single-sign-on). Controleert of dat die Hallo configuratie werkt.

### <a name="set-up-azure-ad-single-sign-on"></a>Instellen van eenmalige aanmelding Azure AD

In deze sectie maakt inschakelen u Azure AD één aanmelding in hello Azure-portal. Vervolgens instellen u eenmalige aanmelding in uw toepassing SAP Business Object Cloud.

tooset van Azure AD eenmalige aanmelding met SAP Business Object Cloud:

1. In de Azure-portal op Hallo Hallo **SAP Business Object Cloud** toepassing Integratiepagina **eenmalige aanmelding**.

    ![Schakel eenmalige aanmelding][4]

2. Op Hallo **eenmalige aanmelding** pagina voor **modus**, selecteer **op basis van SAML aanmelding**.
 
    ![Selecteer op basis van SAML eenmalige aanmelding](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_samlbase.png)

3. Onder **SAP Business Object Cloud-domein en URL's**, volledige Hallo volgende stappen:

    1. In Hallo **aanmeldings-URL** Voer een URL Hallo patroon volgen: 
    | |
    |-|-|
    | `https://<sub-domain>.sapanalytics.cloud/` |
    | `https://<sub-domain>.sapbusinessobjects.cloud/` |

    2. In Hallo **id** Voer een URL Hallo patroon volgen:
    | |
    |-|-|
    | `<sub-domain>.sapbusinessobjects.cloud` |
    | `<sub-domain>.sapanalytics.cloud` |

    ![URL's en SAP Business Object Cloud-domein-URL 's](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_url.png)
 
    > [!NOTE] 
    > Hallo-waarden in deze URL's zijn voor alleen demonstratie. Hallo-waarden bijwerken met de werkelijke Hallo aanmelding URL en de id-URL. tooget hello aanmeldings-URL, neem contact op met Hallo [SAP Business Object Cloud Client ondersteuningsteam](https://www.sap.com/product/analytics/cloud-analytics.support.html). U kunt Hallo identificatie-URL ophalen door Hallo SAP Business Object cloudmetagegevens downloaden vanuit Hallo-beheerconsole. Dit wordt verderop in de zelfstudie Hallo uitgelegd. 

4. Onder **SAML-certificaat voor ondertekening van**, selecteer **Metadata XML**. Sla het metagegevensbestand Hallo op uw computer.

    ![Selecteer de metagegevens-XML](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_certificate.png) 

5. Selecteer **Opslaan**.

    ![Opslaan selecteren](./media/active-directory-saas-sapboc-tutorial/tutorial_general_400.png)

6. Meld u tooyour SAP Business Object Cloud bedrijf site als een beheerder in een ander browservenster.

7. Selecteer **Menu** > **System** > **beheer**.
    
    ![Selecteer vervolgens Menu, systeem en beheer](./media/active-directory-saas-sapboc-tutorial/config1.png)

8. Op Hallo **beveiliging** tabblad, selecteer Hallo **bewerken** pictogram (pen).
    
    ![Selecteer op het tabblad Beveiliging Hallo bewerkingspictogram Hallo](./media/active-directory-saas-sapboc-tutorial/config2.png)  

9. Voor **verificatiemethode**, selecteer **SAML eenmalige aanmelding (SSO)**.

    ![Eenmalige aanmelding SAML voor Hallo verificatiemethode selecteren](./media/active-directory-saas-sapboc-tutorial/config3.png)  

10. toodownload hello serviceprovider metagegevens (stap 1), selecteer **downloaden**. In het metagegevensbestand hello, vindt en kopieert Hallo **id van de entiteit** waarde. In hello Azure portal onder **SAP Business Object Cloud-domein en URL's**, Hallo waarde plakken in Hallo **id** vak.

    ![Kopieer en plak Hallo id van de entiteit waarde](./media/active-directory-saas-sapboc-tutorial/config4.png)  

11. tooupload hello serviceprovider metagegevens (stap 2) in Hallo-bestand dat u hebt gedownload van Azure-portal onder Hallo **identiteitsprovider uploaden metagegevens**, selecteer **uploaden**.  

    ![Selecteer onder de metagegevens van de identiteitsprovider uploaden, uploaden](./media/active-directory-saas-sapboc-tutorial/config5.png)

12. In Hallo **gebruikerskenmerk** wilt weergeven, selecteer Hallo-gebruikerskenmerk (stap 3) wilt u toouse voor uw implementatie. Dit gebruikerskenmerk maps toohello id-provider. een aangepast kenmerk op Hallo van de gebruiker pagina gebruik Hallo tooenter **aangepaste SAML-toewijzing** optie. Of u kunt een selecteren **e** of **gebruikers-ID** als Hallo gebruikerskenmerk. In ons voorbeeld we geselecteerd **e** omdat we Hallo Gebruikersclaim id Hello toegewezen **userprincipalname** kenmerk in Hallo **gebruikerskenmerken** sectie in Hallo Azure-portal. Dit biedt een unieke gebruikers e-mailadres waarmee toohello cloudtoepassing SAP Business-Object in elke geslaagde SAML-reactie wordt verzonden.

    ![Selecteer de gebruiker-kenmerk](./media/active-directory-saas-sapboc-tutorial/config6.png)

13. tooverify Hallo-account met Hallo id-provider (stap 4), in Hallo **aanmelding referentie (E-mail)** Voer het e-mailadres van de gebruiker Hallo. Selecteer **Account controleren**. Hallo-systeem voegt aanmeldingsreferenties toohello gebruikersaccount toe.

    ![Voer e-mailadres en selecteer Account controleren](./media/active-directory-saas-sapboc-tutorial/config7.png)

14. Selecteer Hallo **opslaan** pictogram.

    ![Pictogram opslaan](./media/active-directory-saas-sapboc-tutorial/save.png)

> [!TIP]
> U kunt een beknopte versie van deze instructies in Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u uw app instelt! Nadat u Hallo app door te selecteren toevoegen **Active Directory** > **bedrijfstoepassingen**, selecteer Hallo **Single Sign-On** tabblad. U hebt toegang tot documentatie in Hallo Hallo ingesloten **configuratie** sectie Hallo Hallo pagina onderaan in. Zie voor meer informatie [documentatie van Azure AD ingesloten]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
In deze sectie maakt u een testgebruiker met de naam Britta Simon in hello Azure-portal.

toocreate een testgebruiker in Azure AD:

1. Selecteer in de Azure-portal in het linkermenu Hallo Hallo **Azure Active Directory**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sapboc-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers, selecteer **gebruikers en groepen**, en selecteer vervolgens **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sapboc-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, **toevoegen**.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sapboc-tutorial/create_aaduser_03.png) 

4. In Hallo **gebruiker** dialoogvenster, volledige Hallo stappen te volgen:
 
    1. In Hallo **naam** Voer **BrittaSimon**.

    2. In Hallo **gebruikersnaam** Voer Hallo e-mailadres van de gebruiker Hallo Britta Simon.

    3. Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.

    4. Selecteer **Maken**.

        ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-sapboc-tutorial/create_aaduser_04.png) 

    ![Azure AD-gebruiker maken][100]

### <a name="create-an-sap-business-object-cloud-test-user"></a>Een SAP Business Object Cloud testgebruiker maken

Azure AD-gebruikers moeten worden ingericht in SAP Business Object Cloud voordat ze tooSAP Business Object Cloud kunnen aanmelden. In een SAP Business Object Cloud is inrichting een handmatige taak.

tooprovision een gebruikersaccount:

1. Meld u tooyour SAP Business Object Cloud bedrijf site als beheerder.

2. Selecteer **Menu** > **beveiliging** > **gebruikers**.

    ![Werknemer toevoegen](./media/active-directory-saas-sapboc-tutorial/user1.png)

3. Op Hallo **gebruikers** pagina tooadd nieuwe Gebruikersdetails, selecteer  **+** . 

    ![Gebruikers toevoegen](./media/active-directory-saas-sapboc-tutorial/user4.png)

    Voltooi Hallo stappen te volgen:

    1. In Hallo **gebruikers-ID** Voer Hallo gebruikers-ID van gebruiker hello, zoals **Britta**.

    2. In Hallo **VOORNAAM** Voer Hallo voornaam van de gebruiker hello, zoals **Britta**.

    3. In Hallo **ACHTERNAAM** achternaam op Hallo van Hallo gebruiker, zoals Voer **Simon**.

    4. In Hallo **WEERGAVENAAM** Voer Hallo volledige naam van de gebruiker hello, zoals **Britta Simon**.

    5. In Hallo **e** Voer Hallo e-mailadres van de gebruiker hello, zoals  **brittasimon@contoso.com** .

    6. Op Hallo **rollen selecteren** pagina, selecteer de juiste rol Hallo voor Hallo gebruiker en selecteer vervolgens **OK**.

      ![Rol selecteren](./media/active-directory-saas-sapboc-tutorial/user3.png)

    7. Selecteer Hallo **opslaan** pictogram.  


### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie maakt toestaan u Hallo gebruiker Britta Simon eenmalige aanmelding toouse Azure AD Hallo gebruiker account toegang tooSAP Business Object Cloud verleent.

tooassign Britta Simon tooSAP Business Object Cloud:

1. Hallo toepassingen weergave opent in hello Azure-portal, en gaat u toohello directory weergeven. Selecteer **bedrijfstoepassingen**, en selecteer vervolgens **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **SAP Business Object Cloud**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_app.png) 

3. Selecteer in het linkermenu Hallo **gebruikers en groepen**.

    ![Gebruikers en groepen selecteren][202] 

4. Selecteer **Toevoegen**. Klik vervolgens op Hallo **toevoegen toewijzing** pagina **gebruikers en groepen**.

    ![Hallo toevoegen toewijzing pagina][203]

5. Op Hallo **gebruikers en groepen** pagina in de lijst Hallo van gebruikers, selecteer **Britta Simon**.

6. Op Hallo **gebruikers en groepen** pagina **Selecteer**.

7. Op Hallo **toevoegen toewijzing** pagina **toewijzen**.

![Hallo-gebruikersrollen toewijzen][200] 
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u uw configuratie Azure AD eenmalige aanmelding met behulp van het toegangsvenster Hallo testen.

Wanneer u Hallo SAP Business Object Cloud-tegel in het toegangsvenster Hallo selecteert, moet u tooyour SAP Business Object Cloud-toepassing automatisch worden aangemeld.

Zie voor meer informatie over het toegangsvenster Hallo [inleiding toohello toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het toointegrate SaaS-apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_203.png

