---
title: 'Zelfstudie: Azure Active Directory-integratie met Replicon | Microsoft Docs'
description: Lees hoe toouse Replicon met Azure Active Directory tooenable eenmalige aanmelding, geautomatiseerde inrichting en meer.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 02a62f15-917c-417c-8d80-fe685e3fd601
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 4949eaf959265cfa4f732a2b73317fffe6312a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a>Zelfstudie: Azure Active Directory-integratie met Replicon
Hallo-doel van deze zelfstudie is tooshow Hallo integratie van Azure en Replicon. Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:

* Een geldige Azure-abonnement
* Een tenant Replicon

Na het voltooien van deze zelfstudie worden hello Azure AD-gebruikers die u hebt toegewezen tooReplicon kunnen toosingle Meld u aan bij Hallo-toepassing op uw Replicon bedrijf site (serviceprovider geïnitieerd aanmelding) of met behulp van Hallo [inleiding toohello toegang Deelvenster](active-directory-saas-access-panel-introduction.md).

Hallo scenario beschreven in deze zelfstudie bestaat uit Hallo bouwstenen te volgen:

1. Hallo toepassingsintegratie voor Replicon inschakelen
2. Configureren van eenmalige aanmelding (SSO)
3. Configuratie van gebruikers inrichten
4. Gebruikers toewijzen

![Scenario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Scenario")

## <a name="enable-hello-application-integration-for-replicon"></a>Hallo toepassingsintegratie voor Replicon inschakelen
Hallo-doel van deze sectie is het toooutline hoe tooenable Hallo toepassingsintegratie voor Replicon.

**tooenable hello toepassingsintegratie voor Replicon, Voer Hallo stappen te volgen:**

1. Klik in de klassieke Azure-portal op Hallo navigatiedeelvenster links Hallo op **Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")
2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.
3. tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.
   
    ![Toepassingen](./media/active-directory-saas-replicon-tutorial/IC700994.png "toepassingen")
4. Klik op **toevoegen** Hallo Hallo pagina onderaan in.
   
    ![Toepassing toevoegen](./media/active-directory-saas-replicon-tutorial/IC749321.png "toepassing toevoegen")
5. Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.
   
    ![Een toepassing toevoegen van gallerry](./media/active-directory-saas-replicon-tutorial/IC749322.png "een toepassing van gallerry toevoegen")
6. In Hallo **zoekvak**, type **Replicon**.
   
    ![Toepassingsgalerie](./media/active-directory-saas-replicon-tutorial/IC777799.png "-toepassingsgalerie")
7. Selecteer in het deelvenster met resultaten Hallo **Replicon**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.
   
    ![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")
   
## <a name="configure-single-sign-on"></a>Eenmalige aanmelding configureren

Hallo-doel van deze sectie is toooutline hoe tooenable gebruikers tooauthenticate tooReplicon aan hun account in Azure AD dat gebruikmaakt van Federatie gebaseerd op Hallo SAML-protocol.

**tooconfigure eenmalige aanmelding, voert u Hallo stappen te volgen:**

1. In de klassieke Azure-portal op Hallo Hallo **Replicon** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren eenmalige aanmelding** dialoogvenster.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-replicon-tutorial/IC777801.png "eenmalige aanmelding configureren")
2. Op Hallo **wilt u hoe gebruikers toosign op tooReplicon** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-replicon-tutorial/IC777802.png "eenmalige aanmelding configureren")
3. Op Hallo **App-URL configureren** pagina, voert u Hallo stappen te volgen:
   
    ![App-URL configureren](./media/active-directory-saas-replicon-tutorial/IC777803.png "app-URL configureren")
  1. In Hallo **Replicon aanmelding op URL** textbox, typt u uw Replicon tenant-URL (bijvoorbeeld: *https://na2.replicon.com/company/saml2/sp-sso/post*).
  2. In Hallo **Replicon antwoord-URL** textbox, typt u uw Replicon **AssertionConsumerService** URL (bijvoorbeeld: *https://global.replicon.com/! / saml2/bedrijf/sso/post*).  
      
     >[!NOTE]
     >U kunt Hallo-URL ophalen van Hallo Replicon metagegevens op: **https://global.replicon.com/! /saml2/\<YourCompanyKey\>**.
     > 
     > 
 
  3. Klik op **Volgende**.

4. Op Hallo **eenmalige aanmelding configureren op Replicon** pagina, toodownload uw metagegevens, klikt u op **metagegevens downloaden**, en sla Hallo metagegevens op uw computer.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-replicon-tutorial/IC777804.png "eenmalige aanmelding configureren")
5. In een ander browservenster, meld u bij uw bedrijf Replicon site als beheerder.

6. tooconfigure SAML 2.0, Voer Hallo stappen te volgen:
   
    ![SAML-verificatie inschakelen](./media/active-directory-saas-replicon-tutorial/IC777805.png "inschakelen SAML-verificatie")
  
  1. Hallo toodisplay **EnableSAML Authentication2** dialoogvenster Hallo tooyour-URL te volgen nadat de sleutel van uw bedrijf toevoegen: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**  
    * Hallo hieronder vindt u Hallo-schema van de volledige URL Hallo:  
   **https://Na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**
   2. Klik op Hallo  **+**  tooexpand hello **v20Configuration** sectie.
   3. Klik op Hallo  **+**  tooexpand hello **metaDataConfiguration** sectie.
   4. Klik op **bestand kiezen**, tooselect uw identiteit provider metagegevens-XML-bestand en klik op **indienen**.

7. Op Hallo klassieke Azure-portal, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **Complete** tooclose hello **configureren eenmalige aanmelding** dialoogvenster.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-replicon-tutorial/IC778418.png "eenmalige aanmelding configureren")
   
## <a name="configure-user-provisioning"></a>Gebruikers inrichten configureren

In de volgorde tooenable Azure AD gebruikers toolog in Replicon, moeten ze worden ingericht in Replicon.  

In geval van Replicon Hallo is inrichting een handmatige taak.

**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:**

1. In een browservenster geopend, meld u bij uw bedrijf Replicon site als beheerder.
2. Ga te**beheer \> gebruikers**.
   
    ![Gebruikers](./media/active-directory-saas-replicon-tutorial/IC777806.png "gebruikers")
3. Klik op **+ gebruiker toevoegen**.
   
    ![Gebruiker toevoegen](./media/active-directory-saas-replicon-tutorial/IC777807.png "gebruiker toevoegen")
4. In Hallo **gebruikersprofiel** sectie, voert u Hallo stappen te volgen:
   
    ![Gebruikersprofiel](./media/active-directory-saas-replicon-tutorial/IC777808.png "gebruikersprofiel")
   
  1. In Hallo **aanmeldingsnaam** textbox type hello Azure AD e-mailadres van hello Azure AD-gebruiker die u wilt dat tooprovision.
  2. Als **verificatietype**, selecteer **SSO**.
  3. In Hallo **afdeling** textbox, typ de afdeling Hallo van de gebruiker.
  4. Als **werknemertype**, selecteer **beheerder**.
  5. Klik op **gebruikersprofiel opslaat**.

>[!NOTE]
>U kunt andere Replicon gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Replicon tooprovision AAD-gebruikersaccounts.
> 
> 

## <a name="assign-users"></a>Gebruikers toewijzen
tootest uw configuratie, moet u toogrant hello Azure AD-gebruikers gewenste tooallow met behulp van uw toepassing toegang tooit door toe te wijzen.

**tooassign gebruikers tooReplicon, Hallo volgende stappen uit te voeren:**

1. In de klassieke Azure-portal hello, een testaccount te maken.

2. Op Hallo **Replicon** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.
   
    ![Gebruikers toewijzen](./media/active-directory-saas-replicon-tutorial/IC777809.png "gebruikers toewijzen")

3. Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** tooconfirm de toewijzing.
   
    ![Ja](./media/active-directory-saas-replicon-tutorial/IC767830.png "Ja")

Als u uw instellingen voor eenmalige aanmelding tootest wilt, open Hallo Toegangsvenster. Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

