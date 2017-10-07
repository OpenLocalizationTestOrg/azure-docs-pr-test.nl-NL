---
title: 'Zelfstudie: Azure Active Directory-integratie met identiteitsverificatie voor SAP HANA Cloud Platform | Microsoft Docs'
description: Ontdek hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en SAP HANA Cloud Platform identiteitsverificatie.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c1320d1-7ba4-4b5f-926f-4996b44d9b5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 2142770779ddb745555b47fc85b5457b573f9506
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform-identity-authentication"></a>Zelfstudie: Azure Active Directory-integratie met identiteitsverificatie voor SAP HANA Cloud-Platform

In deze zelfstudie leert u hoe toointegrate SAP HANA Cloud Platform-ID-verificatie met Azure Active Directory (Azure AD). SAP HANA Cloud Platform-ID-verificatie wordt gebruikt als een proxy IdP tooaccess SAP-toepassingen met behulp van Azure AD als belangrijkste IdP Hallo.

SAP HANA Cloud Platform-identiteitsverificatie integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooSAP-toegangstoepassing heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooSAP toepassingen eenmalige aanmelding (SSO) met hun Azure AD-accounts
- U kunt uw accounts op één centrale locatie - Hallo klassieke Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).


## <a name="prerequisites"></a>Vereisten

tooconfigure Azure AD-integratie met identiteitsverificatie voor SAP HANA Cloud-Platform, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een **identiteitsverificatie voor SAP HANA Cloud Platform** SSO abonnement ingeschakeld


>[!NOTE] 
>tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.
>

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een [proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.

Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van identiteitsverificatie voor SAP HANA Cloud Platform van Hallo-galerie
2. Configureren en testen van Azure AD-SSO

Vooraleer Hallo technische gegevens, is het essentieel toounderstand Hallo concepten die u gaat toolook op. Hallo identiteitsverificatie voor SAP HANA Cloud-Platform en Azure Active Directory federation kunt u tooimplement eenmalige aanmelding via toepassingen of services die zijn beveiligd door AAD (als een IdP) met SAP-toepassingen en services die zijn beveiligd door SAP HANA Cloud Platform-identiteit -Verificatie.

Op dit moment fungeert identiteitsverificatie voor SAP HANA Cloud Platform als een Proxy-identiteitsprovider tooSAP-toepassingen. Azure Active Directory wordt op zijn beurt fungeert als Hallo voorloopspaties id-Provider in deze installatie. 

Hallo volgende diagram illustreert dit:    

![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/architecture-01.png)

Met deze instelling wordt uw tenant identiteitsverificatie voor SAP HANA Cloud-Platform worden geconfigureerd als een vertrouwde toepassing in Azure Active Directory. 

Alle SAP-toepassingen en services die u wilt dat tooprotect via deze manier worden vervolgens geconfigureerd in de beheerconsole van Hallo identiteitsverificatie voor SAP HANA Cloud Platform!

Dit betekent dat autorisatie voor het verlenen van toegang tooSAP toepassingen en services-behoeften tootake plaats in identiteitsverificatie voor SAP HANA Cloud Platform voor dergelijke installatie (als tegengestelde tooconfiguring autorisatie in Azure Active Directory).

Identiteitsverificatie voor SAP HANA Cloud Platform configureren als een toepassing via hello Azure Active Directory Marketplace, hoeft u niet tootake antwoord voor het configureren van benodigde afzonderlijke claims / SAML asserties en transformaties nodig tooproduce een geldige verificatietoken voor SAP-toepassingen.

>[!NOTE] 
>Web-SSO is momenteel getest door beide partijen alleen. Stromen nodig voor App-naar-API of API-API-communicatie moeten werken, maar zijn niet getest, nog. Ze worden getest als onderdeel van de volgende activiteiten.
>

## <a name="add-sap-hana-cloud-platform-identity-authentication-from-hello-gallery"></a>Identiteitsverificatie voor SAP HANA Cloud Platform van Hallo galerie toevoegen
tooconfigure hello integratie van identiteitsverificatie voor SAP HANA Cloud-Platform in Azure AD, moet u tooadd identiteitsverificatie voor SAP HANA Cloud Platform uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd SAP HANA Cloud Platform identiteitsverificatie via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo [ **Azure Management portal**](https://portal.azure.com), Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **identiteitsverificatie voor SAP HANA Cloud Platform**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_01.png)

5. Selecteer in het deelvenster resultaten hello, **identiteitsverificatie voor SAP HANA Cloud Platform**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_02.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD
In deze sectie kunt u configureren en testen van Azure AD-SSO met SAP HANA Cloud Platform identiteitsverificatie op basis van een testgebruiker 'Britta Simon' genoemd.

Voor eenmalige aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in identiteitsverificatie voor SAP HANA Cloud Platform is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in identiteitsverificatie voor SAP HANA Cloud Platform toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in identiteitsverificatie voor SAP HANA Cloud-Platform.

tooconfigure en test Azure AD-SSO met identiteitsverificatie voor SAP HANA Cloud-Platform, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van eenmalige aanmelding Azure AD](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker identiteitsverificatie voor SAP HANA Cloud Platform](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)**  -toohave een equivalent van Britta Simon in SAP HANA Cloud Platform verificatie van de identiteit die is gekoppeld toohello Azure AD-weergave van haar.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-sso"></a>Configuratie van Azure AD-SSO

In dit gedeelte Azure AD-eenmalige aanmelding inschakelen in hello Azure Management portal en eenmalige aanmelding configureren in uw toepassing identiteitsverificatie voor SAP HANA Cloud-Platform.

Hallo SAML asserties verwacht identiteitsverificatie voor SAP HANA Cloud Platform toepassing in een specifieke indeling. U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie. Hallo volgende Schermafbeelding toont een voorbeeld voor deze.

![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_03.png)

**Azure AD-SSO met SAP HANA Cloud Platform identiteitsverificatie tooconfigure uitvoeren Hallo stappen te volgen:**

1. In hello Azure Management portal op Hallo **identiteitsverificatie voor SAP HANA Cloud Platform** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren][5]

3. In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster als uw SAP-toepassing een kenmerk bijvoorbeeld 'firstName' wordt verwacht. Voeg op Hallo SAML-token kenmerken dialoogvenster Hallo 'firstName'-kenmerk.
 1. Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.
 
    ![Eenmalige aanmelding configureren][6]

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_05.png)
 2. In Hallo **kenmerknaam** textbox type Hallo kenmerknaam 'firstName'.
 3. Van Hallo **kenmerkwaarde** wilt weergeven, selecteer Hallo kenmerkwaarde 'user.givenname'.
 4. Klik op **OK**.

4. Op Hallo **SAP HANA Cloud Platform identiteit verificatiedomein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_06.png)
 1. In Hallo **aanmelding op URL** textbox, typt u Hallo aanmelding op de URL voor Hallo SAP-toepassing.
 2. In Hallo **id** textbox Hallo typewaarde patroon volgen:`<entity-id>.accounts.ondemand.com` 
    * Als u deze waarde niet weet, volg Hallo identiteitsverificatie voor SAP HANA Cloud Platform documentatie op [Tenantconfiguratie SAML 2.0](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).

5. Op Hallo **SAP HANA Cloud Identity verificatie platformconfiguratie** sectie, klikt u op **configureren SAP HANA Cloud Platform identiteitsverificatie** tooopen **aanmeldingconfigureren** dialoogvenster. Klik vervolgens op **SAML XML-metagegevens** en Hallo-bestand op uw computer op te slaan.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_07.png) 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_08.png)

6. tooget SSO is geconfigureerd voor uw toepassing gaat tooSAP HANA Cloud Platform identiteit verificatie-beheerconsole. Hallo-URL heeft Hallo patroon volgen:`https://<tenant-id>.accounts.ondemand.com/admin`
 * Volg Hallo-documentatie op identiteitsverificatie voor SAP HANA Cloud Platform te[Configure Microsoft Azure AD als zakelijke id-Provider op identiteitsverificatie voor SAP HANA Cloud Platform](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html). 

7. Klik in hello Azure Management portal op **opslaan** knop.
8. Volgende stappen uit als u tooadd wilt en eenmalige aanmelding voor een andere SAP-toepassing inschakelen hello blijven. Herhaal de stappen onder Hallo sectie 'Toevoegen SAP HANA Cloud Platform identiteitsverificatie uit de galerie Hallo' tooadd een ander exemplaar van identiteitsverificatie voor SAP HANA Cloud-Platform.
9. In hello Azure Management portal op Hallo **identiteitsverificatie voor SAP HANA Cloud Platform** toepassing Integratiepagina, klikt u op **gekoppelde aanmelding**.

    ![Gekoppelde aanmelding configureren](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/linked_sign_on.png)
10. Vervolgens Hallo-configuratie op te slaan.

>[!NOTE] 
>de nieuwe toepassing Hello wordt Hallo SSO-configuratie voor de vorige SAP-toepassing hello gebruikmaken. Controleer of u gebruik Hallo dezelfde zakelijke identiteitsproviders in Hallo SAP HANA Cloud Platform identiteit verificatie-beheerconsole.
>

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in de nieuwe portal Hallo Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_01.png) 

2. Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_02.png) 

3. Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_04.png) 
  1. In Hallo **naam** textbox type **BrittaSimon**.
  2. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.
  3. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.
  4. Klik op **Create**. 

### <a name="create-a-sap-hana-cloud-platform-identity-authentication-test-user"></a>Maak een testgebruiker identiteitsverificatie voor SAP HANA Cloud-Platform

U hoeft niet toocreate een gebruiker op identiteitsverificatie voor SAP HANA Cloud-Platform. Gebruikers die zich in het archief hello Azure AD-gebruiker kunnen Hallo SSO-functies gebruiken.

SAP HANA Cloud Platform-identiteitsverificatie ondersteunt Hallo identiteitsfederatie optie. Deze optie kunt Hallo toepassing toocheck als Hallo gebruikers door de zakelijke identiteitsprovider Hallo geverifieerde in Hallo store van SAP HANA Cloud Platform identiteit gebruikersverificatie. 

In de standaardinstelling Hallo is Hallo identiteitsfederatie optie uitgeschakeld. Als identiteitsfederatie is ingeschakeld, zijn alleen Hallo-gebruikers die worden geïmporteerd in identiteitsverificatie voor SAP HANA Cloud-Platform kunnen tooaccess Hallo-toepassing. 

Voor meer informatie over hoe tooenable of schakelt u identiteitsfederatie met SAP HANA Cloud Platform identiteitsverificatie, identiteitsfederatie inschakelen met SAP HANA Cloud Platform identiteitsverificatie in zien [identiteitsfederatie configureren Hello Store van SAP HANA Cloud Platform identiteit gebruikersverificatie. ](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar toegang tooSAP HANA Cloud Platform identiteitsverificatie verlenen.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooSAP HANA Cloud Platform identiteitsverificatie Hallo stappen uitvoeren:**

1. Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **identiteitsverificatie voor SAP HANA Cloud Platform**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_09.png)

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    

### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u uw Azure AD SSO-configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo identiteitsverificatie voor SAP HANA Cloud Platform-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour identiteitsverificatie voor SAP HANA Cloud Platform-toepassing.


## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_06.png

[100]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_203.png