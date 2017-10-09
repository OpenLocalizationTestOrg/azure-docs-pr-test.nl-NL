---
title: 'Zelfstudie: Azure Active Directory-integratie met TOPdesk - beveiligde | Microsoft Docs'
description: Meer informatie over hoe toouse TOPdesk - beveiligen met Azure Active Directory tooenable eenmalige aanmelding, geautomatiseerde inrichting en meer!.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 8e149d2d-7849-48ec-9993-31f4ade5fdb4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 10fe420d1691c2845b89c779486ffd6fcd736432
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a>Zelfstudie: Azure Active Directory-integratie met TOPdesk - beveiligen
Hallo-doel van deze zelfstudie is tooshow Hallo integratie van Azure en TOPdesk - beveiligen.  
Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:

* Een geldige Azure-abonnement
* Een TOPdesk - beveiligde eenmalige aanmelding ingeschakeld abonnement

Na het voltooien van deze zelfstudie, hello Azure AD-gebruikers hebt u tooTOPdesk - beveiligde wordt toegewezen worden kunnen toosingle Meld u aan bij de toepassing hello op uw TOPdesk - beveiligd bedrijf site (serviceprovider geïnitieerd aanmelding) of met behulp van Hallo [Inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

Hallo scenario beschreven in deze zelfstudie bestaat uit Hallo bouwstenen te volgen:

1. Hallo toepassingsintegratie voor TOPdesk - beveiligde inschakelen
2. Eenmalige aanmelding configureren
3. Configuratie van gebruikers inrichten
4. Gebruikers toewijzen

![Scenario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scenario")

## <a name="enabling-hello-application-integration-for-topdesk---secure"></a>Hallo toepassingsintegratie voor TOPdesk - beveiligde inschakelen
Hallo-doel van deze sectie is het toooutline hoe tooenable Hallo toepassingsintegratie voor TOPdesk - veilig.

### <a name="tooenable-hello-application-integration-for-topdesk---secure-perform-hello-following-steps"></a>tooenable hello toepassingsintegratie voor TOPdesk - wilt beveiligen, voert u Hallo stappen te volgen:
1. Klik in de klassieke Azure-portal op Hallo navigatiedeelvenster links Hallo op **Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")

2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.

3. tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.
   
    ![Toepassingen](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "toepassingen")

4. Klik op **toevoegen** Hallo Hallo pagina onderaan in.
   
    ![Toepassing toevoegen](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "toepassing toevoegen")

5. Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.
   
    ![Een toepassing toevoegen van gallerry](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "een toepassing van gallerry toevoegen")

6. In Hallo **zoekvak**, type **TOPdesk - beveiligde**.
   
    ![Toepassingsgalerie](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "-Toepassingsgalerie")

7. Selecteer in het deelvenster met resultaten Hallo **TOPdesk - beveiligde**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.
   
    ![TOPdesk - beveiligde](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - beveiligen")

## <a name="configuring-single-sign-on"></a>Eenmalige aanmelding configureren
Hallo-doel van deze sectie is het toooutline hoe tooenable gebruikers tooauthenticate tooTOPdesk - beveiligen met een account in Azure AD dat gebruikmaakt van Federatie op basis van Hallo SAML-protocol.  
Vereist de tooupload een pictogrambestand logo configureren eenmalige aanmelding voor TOPdesk - veilig. tooget pictogrambestand hello, neem contact op met Hallo TOPdesk ondersteuningsteam.

### <a name="tooconfigure-single-sign-on-perform-hello-following-steps"></a>tooconfigure eenmalige aanmelding, voert u Hallo stappen te volgen:
1. Meld u aan bij tooyour **TOPdesk - beveiligde** bedrijf site als beheerder.
2. In Hallo **TOPdesk** menu, klikt u op **instellingen**.
   
    ![Instellingen](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "instellingen")

3. Klik op **aanmeldingsinstellingen**.
   
    ![Instellingen voor aanmelding](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "aanmeldingsinstellingen")

4. Vouw Hallo **aanmeldingsinstellingen** menu en klik vervolgens op **algemene**.
   
    ![Algemene](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "algemeen")

5. In Hallo **Secure** sectie Hallo **SAML aanmelding** configuratie sectie, voert u Hallo stappen te volgen:
   
    ![Instellingen voor technische](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "technische instellingen")
   
    a. Klik op **downloaden** toodownload openbare metagegevensbestand Hallo en lokaal opslaan op uw computer.
   
    b. Open metagegevensbestand hello, en Ga naar Hallo **AssertionConsumerService** knooppunt.
    
    ![Verklaring Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer-Service")
   
    c. Kopiëren Hallo **AssertionConsumerService** waarde.  
      
    > [!NOTE]
    > U moet Hallo waarde in Hallo **App-URL configureren** verderop in deze zelfstudie.
    > 
    > 

6. In een ander browservenster, meld u aan bij uw **klassieke Azure-portal** als beheerder.

7. Op Hallo **TOPdesk - beveiligde** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen Hallo ** configureren eenmalige aanmelding ** dialoogvenster.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "eenmalige aanmelding configureren")

8. Op Hallo **hoe wilt u beveiligen zoals gebruikers toosign op tooTOPdesk -** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "eenmalige aanmelding configureren")

9. Op Hallo **App-URL configureren** pagina, voert u Hallo stappen te volgen:
   
    ![App-URL configureren](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "App-URL configureren")
   
    a. In Hallo **TOPdesk - beveiligde aanmelding op URL** textbox type Hallo-URL die door uw gebruikers toosign wordt gebruikt in uw TOPdesk - beveiligde toepassing (bijvoorbeeld: '*https://qssolutions.topdesk.net*').
   
    b. In Hallo **TOPdesk – openbare antwoord-URL** textbox plakken Hallo **TOPdesk - beveiligde AssertionConsumerService URL** (bijvoorbeeld: '*https://qssolutions.topdesk.net/tas/public/login/saml*")
   
    c. Klik op **Volgende**.

10. Op Hallo **eenmalige aanmelding configureren op TOPdesk - beveiligde** pagina, toodownload uw bestand met metagegevens, klikt u op **metagegevens downloaden**, en sla Hallo bestand lokaal op uw computer.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "eenmalige aanmelding configureren")

11. een certificaatbestand toocreate uitvoeren Hallo stappen te volgen:
    
    ![Certificaat](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "certificaat")
    
    a. Open Hallo gedownloade metagegevensbestand.
    b. Vouw Hallo **RoleDescriptor** knooppunt met een **xsi: type** van **ingevoerd: ApplicationServiceType**.
    c. Kopieer de waarde Hallo Hallo **X509Certificate** knooppunt.
    d. Opslaan Hallo gekopieerd **X509Certificate** waarde lokaal op uw computer in een bestand.

12. Op uw TOPdesk - beveiligd bedrijf site in Hallo **TOPdesk** menu, klikt u op **instellingen**.
    
    ![Instellingen](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "instellingen")

13. Klik op **aanmeldingsinstellingen**.
    
    ![Instellingen voor aanmelding](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "aanmeldingsinstellingen")

14. Vouw Hallo **aanmeldingsinstellingen** menu en klik vervolgens op **algemene**.
    
    ![Algemene](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "algemeen")

15. In Hallo **openbare** sectie, klikt u op **toevoegen**.
    
    ![Voeg](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "toevoegen")

16. Op Hallo **SAML-configuratie-assistent** dialoogvenster pagina, voert u Hallo stappen te volgen:
    
    ![SAML-configuratie-assistent](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "assistent voor SAML-configuratie")
    
    a. de metagegevens van het gedownloade bestand, onder tooupload **Federatiemetagegevens**, klikt u op **Bladeren**.

    b. uw certificaat bestand onder tooupload **certificaat (RSA)**, klikt u op **Bladeren**.

    c. tooupload Hallo logo-bestand die u hebt gekregen Hallo TOPdesk ondersteuningsteam, onder **Logo pictogram**, klikt u op **Bladeren**.

    d. In Hallo **naam gebruikerskenmerk** textbox type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.

    e. In Hallo **weergavenaam** textbox, typ een naam voor uw configuratie.

    f. Klik op **Opslaan**.

17. Op Hallo klassieke Azure-portal, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **Complete** tooclose hello **configureren eenmalige aanmelding** dialoogvenster.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "eenmalige aanmelding configureren")

## <a name="configuring-user-provisioning"></a>Configuratie van gebruikers inrichten
In de volgorde tooenable Azure AD-gebruikers toolog in TOPdesk - veilige, ze moeten worden ingericht in TOPdesk - veilig.  
In geval van TOPdesk - Hallo veilige, inrichting is een handmatige taak.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:
1. Meld u aan bij tooyour **TOPdesk - beveiligde** bedrijf site als administrator.
2. Klik in het menu bovenaan Hallo Hallo **TOPdesk \> nieuw \> ondersteuningsbestanden \> Operator**.
   
    ![Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator")

3. Op Hallo **Operator New** dialoogvenster Hallo volgende stappen uit te voeren:
   
    ![Nieuwe Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "nieuwe Operator")
   
    a. Klik op tabblad Algemeen van Hallo.
   
    b. In Hallo **achternaam** textbox Hallo **algemene** sectie, type Hallo achternaam van een geldige Azure Active Directory-account dat u wilt dat tooprovision.
   
    c. Selecteer een **Site** voor Hallo-account in Hallo **locatie** sectie.
   
    d. In Hallo **aanmeldingsnaam** textbox Hallo **TOPdesk aanmelding** sectie, typt u een aanmeldingsnaam voor de gebruiker.
   
    e. Klik op **Opslaan**.

> [!NOTE]
> U kunt andere TOPdesk - beveiligde gebruikersaccount hulpmiddelen voor het maken of API's die worden geleverd door TOPdesk - Secure tooprovision AAD-gebruikersaccounts gebruiken.
> 
> 

## <a name="assigning-users"></a>Gebruikers toewijzen
tootest uw configuratie, moet u toogrant hello Azure AD-gebruikers gewenste tooallow met behulp van uw toepassing toegang tooit door toe te wijzen.

### <a name="tooassign-users-tootopdesk---secure-perform-hello-following-steps"></a>tooassign gebruikers tooTOPdesk - beveiligen, voert u Hallo stappen te volgen:
1. In de klassieke Azure-portal hello, een testaccount te maken.
2. Op Hallo ** TOPdesk - beveiligde ** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.
   
    ![Gebruikers toewijzen](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "gebruikers toewijzen")

3. Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** tooconfirm de toewijzing.
   
    ![Ja](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Ja")

Als u uw instellingen voor eenmalige aanmelding tootest wilt, open Hallo Toegangsvenster. Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

