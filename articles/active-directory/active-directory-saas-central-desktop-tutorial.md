---
title: 'Zelfstudie: Azure Active Directory-integratie met centraal bureaublad | Microsoft Docs'
description: Lees hoe toouse centrale bureaublad met Azure Active Directory tooenable eenmalige aanmelding, geautomatiseerde inrichting en meer.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: b805d485-93db-49b4-807a-18d446c7090e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 93036ae801c446ce476288c00579931ba10a843b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a>Zelfstudie: Azure Active Directory-integratie met centraal bureaublad
Hallo-doel van deze zelfstudie is tooshow Hallo integratie van Azure en centrale bureaublad. Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:

* Een geldige Azure-abonnement
* Een centrale bureaublad eenmalige aanmelding ingeschakeld abonnement / tenant-centrale bureaublad

Hallo scenario beschreven in deze zelfstudie bestaat uit Hallo bouwstenen te volgen:

* Hallo toepassingsintegratie voor centrale bureaublad inschakelen
* Configureren van eenmalige aanmelding (SSO)
* Configuratie van gebruikers inrichten
* Gebruikers toewijzen

![Scenario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scenario")

## <a name="enable-hello-application-integration-for-central-desktop"></a>Integratie van Hallo-toepassing voor centrale bureaublad inschakelen
Hallo-doel van deze sectie is het toooutline hoe tooenable Hallo toepassingsintegratie voor centrale bureaublad.

**tooenable hello toepassingsintegratie voor centrale bureaublad Hallo stappen uitvoeren:**

1. Klik in de klassieke Azure-portal op Hallo navigatiedeelvenster links Hallo op **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")
2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.
3. tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.
   
   ![Toepassingen](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "toepassingen")
4. Klik op **toevoegen** Hallo Hallo pagina onderaan in.
   
   ![Toepassing toevoegen](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "toepassing toevoegen")
5. Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.
   
   ![Een toepassing toevoegen van gallerry](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "een toepassing van gallerry toevoegen")
6. In Hallo **zoekvak**, type **centrale bureaublad**.
   
   ![Toepassingsgalerie](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "-toepassingsgalerie")
7. Selecteer in het deelvenster met resultaten Hallo **centrale bureaublad**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.
   
   ![Centrale bureaublad](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "centrale bureaublad")
   
## <a name="configure-single-sign-on"></a>Eenmalige aanmelding configureren

Hallo-doel van deze sectie is toooutline hoe tooenable gebruikers tooauthenticate tooCentral bureaublad aan hun account in Azure AD dat gebruikmaakt van Federatie gebaseerd op Hallo SAML-protocol.

Als onderdeel van deze procedure bent u vereiste tooupload een Base64-gecodeerde certificaat tooyour centrale Desktop-tenant.  
Als u niet bekend met deze procedure bent, Zie [hoe tooconvert een binair bestand van het certificaat naar een tekstbestand](http://youtu.be/PlgrzUZ-Y1o).

**tooconfigure eenmalige aanmelding, voert u Hallo stappen te volgen:**

1. In de klassieke Azure-portal op Hallo Hallo **centrale bureaublad** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen Hallo ** configureren eenmalige aanmelding ** dialoogvenster.
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "eenmalige aanmelding configureren")
2. Op Hallo **wilt u hoe gebruikers toosign op tooCentral bureaublad** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "eenmalige aanmelding configureren")
3. Op Hallo **App-URL configureren** pagina, het uitvoeren van Hallo volgende stappen uit en klik vervolgens op **volgende**: 
   
   1. In Hallo **centrale bureaublad aanmelding In URL** textbox type Hallo-URL van uw tenant centrale bureaublad (bijvoorbeeld: *http://contoso.centraldesktop.com*).
   2. In een tekstvak Hallo centrale bureaublad antwoord-URL, typt u uw centrale bureaublad AssertionConsumerService URL (bijvoorbeeld: https://contoso.centraldesktop.com/saml2-assertion.php).
   
   >[!NOTE]
   >U kunt benutten Hallo Hallo centrale bureaublad metagegevens (bijvoorbeeld: *http://contoso.centraldesktop.com*).
   >  
   
   ![App-URL configureren](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "app-URL configureren")
4. Op Hallo **op centrale bureaublad eenmalige aanmelding configureren** pagina, toodownload uw certificaat, klik op **certificaat downloaden**, en sla het Hallo-certificaatbestand op uw computer.
   
  ![Eenmalige aanmelding configureren](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "eenmalige aanmelding configureren")
5. Meld u bij tooyour **centrale bureaublad** tenant.
6. Ga te**instellingen**, klikt u op **Geavanceerd**, en klik vervolgens op **eenmalige aanmelding**.
   
  ![Setup - geavanceerde](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Setup - geavanceerde")
7. Op Hallo **eenmalige aanmelding op instellingen** pagina, voert u Hallo stappen te volgen:
   
  ![Eenmalige aanmelding instellingen](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "eenmalige van instellingen")
   
  1. Selecteer **inschakelen SAML v2 voor eenmalige aanmelding**.
  2. In de klassieke Azure-portal op Hallo Hallo **eenmalige aanmelding configureren op de centrale bureaublad** pagina, kopie Hallo **URL-verlener** waarde en plak deze in Hallo **URL SSO** textbox.
  3. In de klassieke Azure-portal op Hallo Hallo **eenmalige aanmelding configureren op de centrale bureaublad** pagina, kopie Hallo **externe aanmeldings-URL** waarde en plak deze in Hallo **aanmeldings-URL voor eenmalige aanmelding**textbox.
  4. In de klassieke Azure-portal op Hallo Hallo **eenmalige aanmelding configureren op de centrale bureaublad** pagina, kopie Hallo **Service-URL met eenmalige Sign-Out** waarde en plak deze in Hallo **SSO afmelding URL** textbox.
8. In Hallo **bericht handtekening verificatiemethode** sectie, voert u Hallo stappen te volgen:
   
   ![Handtekening verificatiemethode bericht](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "bericht handtekening verificatiemethode")
   
  1. Selecteer **certificaat**.
  2. Van Hallo **SSO certificaat** selecteert **RSH SHA256**.
  3. Maak een tekstbestand van Hallo gedownload certificaat, kopie Hallo inhoud van het tekstbestand hello, en plak deze in Hallo **SSO certificaat** veld.  
     >[!TIP]
     >Zie voor meer informatie [hoe tooconvert een binair bestand van het certificaat naar een tekstbestand](http://youtu.be/PlgrzUZ-Y1o)
      >  
   4. Selecteer **een koppeling tooyour SAMLv2-aanmeldingspagina weergegeven**.
9. Klik op **Update**.
10. Op Hallo klassieke Azure-portal, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **Complete** tooclose hello **configureren eenmalige aanmelding** dialoogvenster.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "eenmalige aanmelding configureren")
    
## <a name="configure-user-provisioning"></a>Gebruikers inrichten configureren

Voor AAD gebruikers toobe kunnen toosign in, moeten ze ingerichte toohello centrale bureaubladtoepassingen zijn. Deze sectie beschrijft hoe toocreate AAD gebruikersaccounts in centrale bureaublad.

**tooprovision gebruiker accounts tooCentral bureaublad:**
1. Meld u bij tooyour centrale bureaublad tenant.
2. Ga te**mensen \> interne leden**.
3. Klik op **interne leden toevoegen**.
   
  ![Mensen](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "personen")
4. In Hallo **e-mailadres van nieuwe leden** textbox, typt u een AAD-account u wilt tooprovision en klik vervolgens op **volgende**.
   
  ![E-mailadressen van nieuwe leden](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "e-mailadressen van nieuwe leden")
5. Klik op **interne toevoegen leden**.
   
  ![Interne lid toevoegen](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "interne lid toevoegen")
   
   >[!NOTE]
   >Hallo-gebruikers die u hebt toegevoegd, ontvangt een e-mailbericht met een bevestigingskoppeling ze tooclick tooactivate Hallo-account nodig.
   > 

>[!NOTE]
>U kunt andere centrale bureaublad gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door centrale bureaublad tooprovision AAD-gebruikersaccounts
>  

## <a name="assign-users"></a>Gebruikers toewijzen
tootest uw configuratie, moet u toogrant hello Azure AD-gebruikers gewenste tooallow met behulp van uw toepassing toegang tooit door toe te wijzen.

**tooassign gebruikers tooCentral bureaublad Hallo stappen uitvoeren:**

1. In de klassieke Azure-portal hello, een testaccount te maken.
2. Op Hallo **centrale bureaublad** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.
   
   ![Gebruikers toewijzen](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "gebruikers toewijzen")
3. Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** tooconfirm de toewijzing.
   
   ![Ja](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Ja")

Als u uw instellingen voor eenmalige aanmelding tootest wilt, open Hallo Toegangsvenster. Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

