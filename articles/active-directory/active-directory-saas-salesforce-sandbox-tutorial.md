---
title: 'Zelfstudie: Azure Active Directory-integratie met Salesforce Sandbox | Microsoft Docs'
description: Meer informatie over hoe toouse Salesforce Sandbox met Azure Active Directory tooenable eenmalige aanmelding, geautomatiseerde inrichting en meer!.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: deccd6a07b57c8ba56b7e1c3f3ab311813ca017b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a>Zelfstudie: Azure Active Directory-integratie met Salesforce Sandbox

Hallo-doel van deze zelfstudie is tooshow Hallo integratie van Azure en Salesforce Sandbox.  

>[!TIP]
>Zie voor feedback over Hallo [Azure ondersteuningspagina](http://go.microsoft.com/fwlink/?LinkId=521878). 
> 

Sandboxes geven u Hallo mogelijkheid toocreate meerdere kopieën van uw organisatie in een afzonderlijke omgeving voor verschillende doeleinden, zoals ontwikkeling, testen en training, zonder in gevaar te brengen Hallo gegevens en toepassingen in uw productieomgeving Salesforce de organisatie.  

Zie voor meer informatie [sandbox-overzicht](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)

Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:

* Een geldige Azure-abonnement
* Een sandbox in Salesforce.com

Als u nog een geldige sandbox in Salesforce.com hebt, moet u toocontact Salesforce.

Hallo scenario beschreven in deze zelfstudie bestaat uit Hallo bouwstenen te volgen:

1. Hallo toepassingsintegratie voor Salesforce Sandbox inschakelen
2. Configureren van eenmalige aanmelding (SSO)
3. Uw domein inschakelen
4. Configuratie van gebruikers inrichten
5. Gebruikers toewijzen

![Scenario](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Scenario")

## <a name="enable-hello-application-integration-for-salesforce-sandbox"></a>Hallo toepassingsintegratie voor Salesforce Sandbox inschakelen
Hallo-doel van deze sectie is het toooutline hoe tooenable Hallo toepassingsintegratie voor Salesforce sandbox.

**tooenable hello toepassingsintegratie voor Salesforce-sandbox Hallo stappen uitvoeren:**

1. Klik in de klassieke Azure-portal op Hallo navigatiedeelvenster links Hallo op **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")
2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.
3. tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.
   
   ![Toepassingen](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "toepassingen")
4. Hallo tooopen **Toepassingsgalerie**, klikt u op **een App toevoegen**, en klik vervolgens op **toevoegen van een toepassing voor mijn organisatie toouse**.
   
   ![Wat wilt u wilt dat toodo? ] (./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "Wat wilt u wilt dat toodo?")
5. In Hallo **zoekvak**, type **Salesforce Sandbox**.
   
   ![Toepassingsgalerie](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "-Toepassingsgalerie")
6. Selecteer in het deelvenster met resultaten Hallo **Salesforce Sandbox**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.
   
   ![SalesForce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")
   
## <a name="configur-single-sign-on-sso"></a>Configur eenmalige aanmelding (SSO)

Hallo-doel van deze sectie is toooutline hoe tooenable gebruikers tooauthenticate tooSalesforce aan hun account in Azure AD dat gebruikmaakt van Federatie gebaseerd op Hallo SAML-protocol.

**tooconfigure eenmalige aanmelding, voert u Hallo stappen te volgen:**

1. In de klassieke Azure-portal op Hallo Hallo **Salesforce Sandbox** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren eenmalige aanmelding** het dialoogvenster.
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "eenmalige aanmelding configureren")
2. Op Hallo **wilt u hoe gebruikers toosign op tooSalesforce Sandbox** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.
   
   ![SalesForce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")
3. Op Hallo **App-URL configureren** pagina in Hallo **aanmelding op URL** textbox, typt u uw URL Hallo patroon volgen met `http://company.my.salesforce.com`, en klik vervolgens op **volgende**.
   
   ![App-URL configureren](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "App-URL configureren")
4. Als u al eenmalige aanmelding voor een ander exemplaar van Salesforce Sandbox hebt geconfigureerd in uw directory, dan moet u ook Hallo configureren **id** toohave dezelfde waarde als Hallo Hallo **aanmelden URL**. 
 * Hallo **id** veld kan worden gevonden door te controleren Hallo **weergeven geavanceerde instellingen** selectievakje op Hallo **App-URL configureren** van Hallo-menu.
5. Op Hallo **eenmalige aanmelding configureren op de Salesforce Sandbox** pagina, klikt u op **certificaat downloaden**, en sla het Hallo-certificaatbestand op uw computer.
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "eenmalige aanmelding configureren")
6. In een ander browservenster, meld u bij uw Salesforce-sandbox als beheerder.
7. Klik in het menu bovenaan Hallo Hallo **Setup**.
   
   ![Setup](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Setup")
8. Klik in het navigatievenster aan de linkerkant Hallo Hallo op **beveiligingsmechanismen**, en klik vervolgens op **instellingen voor eenmalige aanmelding**.
   
   ![Eenmalige aanmelding instellingen](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "eenmalige aanmelding-instellingen")
9. Op Hallo sectie instellingen voor eenmalige aanmelding, voert u Hallo stappen te volgen:
   
   ![Eenmalige aanmelding instellingen](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "eenmalige aanmelding-instellingen")  
 1.  Selecteer **SAML ingeschakeld**. 
 2.  Klik op **Nieuw**.
10. Op Hallo SAML Single Sign-On zoekinstellingen, voert u Hallo stappen te volgen:
    
    ![SAML eenmalige aanmelding-instellingen](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML eenmalige aanmelding-instellingen")  
 1. Typ in Hallo naam textbox Hallo-naam van Hallo-configuratie (bijvoorbeeld: *SPSSOWAAD\_Test*). 
 2. In de klassieke Azure-portal op Hallo Hallo **eenmalige aanmelding configureren op de Salesforce Sandbox** dialoog pagina, kopie Hallo **URL-verlener** waarde en plak deze in Hallo **verlener**textbox.
 3. In Hallo **entiteit-Id** textbox type **https://test.salesforce.com** als het Hallo eerste Salesforce sandbox-exemplaar dat u tooyour directory toevoegt. Als u al een exemplaar van Salesforce Sandbox, moet u voor Hallo hebt toegevoegd **entiteit-ID** type in Hallo **aanmelding op URL**, die moet worden in deze indeling:`http://company.my.salesforce.com`   
 4. Klik op **Bladeren** tooupload Hallo certificaat gedownload.  
 5. Als **SAML identiteitstype**, selecteer **Assertion bevat Hallo Federatie-ID van het gebruikersobject Hallo**. 
 6. Als **SAML identiteit locatie**, selecteer **identiteit is in Hallo NameIdentifier element van Hallo onderwerp instructie**.
 7. In de klassieke Azure-portal op Hallo Hallo **eenmalige aanmelding configureren op de Salesforce Sandbox** dialoog pagina, kopie Hallo **externe aanmeldings-URL** waarde en plak deze in Hallo **id-Provider Aanmeldings-URL** textbox. 
 8. SFDC biedt geen ondersteuning voor SAML-afmelden.  Als een tijdelijke oplossing 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' te plakken in Hallo **identiteit Provider afmelding URL** textbox.
 9. Als **Provider geïnitieerd aanvragen servicebinding**, selecteer **HTTP POST**. 
 10. Klik op **Opslaan**.
11. Op Hallo klassieke Azure-portal, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **Complete** tooclose hello **configureren eenmalige aanmelding** dialoogvenster.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "eenmalige aanmelding configureren")

## <a name="enable-your-domain"></a>Uw domein inschakelen
Deze sectie wordt ervan uitgegaan dat u al hebt gemaakt een domein.  Zie voor meer informatie [definiëren van uw domeinnaam](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).

**tooenable uw domein Hallo volgende stappen uit te voeren:**

1. Klik in het Hallo navigatiedeelvenster links op **domeinbeheer**, en klik vervolgens op **mijn domein.**
   
   ![Mijn domein](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "mijn domein")
   
   >[!NOTE]
   >Zorg dat uw domein correct is geconfigureerd. 
   > 
2. In Hallo **aanmelding paginainstellingen** sectie, klikt u op **bewerken**, naarmate **verificatieservice**, selecteer Hallo-naam van Hallo SAML Single Sign-On-instelling van de vorige Hallo sectie en ten slotte op **opslaan**.
   
   ![Mijn domein](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "mijn domein")

Als u een domein geconfigureerd hebt, moeten uw gebruikers Hallo domein URL toologin toohello Salesforce sandbox gebruiken.  

tooget Hallo waarde van de URL van de hello, klikt u op Hallo SSO profiel die u hebt gemaakt in de vorige sectie Hallo.

## <a name="configure-user-provisioning"></a>Gebruikers inrichten configureren
Hallo-doel van deze sectie is het toooutline hoe tooenable gebruikers inrichten van Active Directory-gebruiker accounts tooSalesforce Sandbox.

**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:**

1. Selecteer in de bovenste navigatiebalk Hallo van Hallo Salesforce Portal uw naam tooexpand uw gebruikersmenu:
   
   ![Mijn instellingen](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "Mijn instellingen")
2. Selecteer in het gebruikersmenu **Mijn instellingen** tooopen uw **Mijn instellingen** pagina.
3. Klik in het linkerdeelvenster Hallo **persoonlijke** tooexpand Hallo persoonlijke sectie en klik vervolgens op **opnieuw mijn beveiligingstoken**:
   
   ![Mijn instellingen](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "Mijn instellingen")
4. Op Hallo **opnieuw mijn beveiligingstoken** pagina, klikt u op **Security Token opnieuw** toorequest een e-mailbericht met uw beveiligingstoken Salesforce.com.
   
   ![Nieuw Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "nieuw Token")
5. Controleer uw postvak voor een e-mailbericht van Salesforce.com met '**salesforce.com.com beveiligingsgegevens**' als onderwerp.
6. Bekijk deze e-mail en kopiëren hello security token waarde.
7. In de klassieke Azure-portal op Hallo Hallo **salesforce Sandbox** pagina van de integratie van toepassing, klikt u op **configureren gebruikersaanvragen** tooopen hello **configureren gebruikersaanvragen**dialoogvenster.
   
   ![Configureer gebruikersaanvragen](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "gebruikers inrichten configureren")
8. Op Hallo **Voer uw Salesforce-Sandbox referenties tooenable automatisch gebruikers inrichten** pagina, bieden Hallo na configuratie-instellingen:
   
   ![SalesForce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")   
 1. In Hallo **Salesforce Sandbox-Beheerdersgebruikersnaam** textbox type een sandbox met Salesforce accountnaam die heeft Hallo **systeembeheerder** profiel in Salesforce.com toegewezen.
 2. In Hallo **Salesforce Sandbox beheerderswachtwoord** textbox Hallo een wachtwoord op voor dit account.
 3. In Hallo **gebruiker beveiligingstoken** textbox plakken hello security token waarde.
 4. Klik op **valideren** tooverify uw configuratie.
 5. Klik op Hallo **volgende** knop tooopen hello **bevestiging** pagina.
9. Op Hallo **bevestiging** pagina, klikt u op **Complete** toosave uw configuratie.
   
## <a name="assigning-users"></a>Gebruikers toewijzen

tootest uw configuratie, moet u toogrant hello Azure AD-gebruikers gewenste tooallow met behulp van uw toepassing toegang tooit door toe te wijzen.

**tooassign gebruikers tooSalesforce Sandbox, Voer Hallo stappen te volgen:**

1. In de klassieke Azure-portal hello, een testaccount te maken.
2. Op Hallo ** Salesforce Sandbox ** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.
   
   ![Gebruikers toewijzen](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "gebruikers toewijzen")
3. Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** tooconfirm de toewijzing.
   
   ![Ja](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Ja")

U moet nu wacht tien minuten en controleren of de Hallo-account is gesynchroniseerd tooSalesforce Sandbox.

Als u uw instellingen SSO tootest wilt, open Hallo Toegangsvenster. Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](https://msdn.microsoft.com/library/dn308586).

