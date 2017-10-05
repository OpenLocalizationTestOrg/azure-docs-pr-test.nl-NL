---
title: 'Zelfstudie: Azure Active Directory-integratie met SAP HANA-Cloudplatform | Microsoft Docs'
description: Meer informatie over het SAP HANA Cloud-Platform gebruiken met Azure Active Directory om te schakelen van eenmalige aanmelding, geautomatiseerde inrichting en meer!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: bd398225-8bd8-4697-9a44-af6e6679113a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: e03bc2410a8d57363c558f723b3bfd0e69b3f4c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a>Zelfstudie: Azure Active Directory-integratie met SAP HANA-cloudplatform
Het doel van deze zelfstudie is het weergeven van de integratie van Azure en SAP HANA-Cloud-Platform.

Het scenario in deze zelfstudie wordt ervan uitgegaan dat u al de volgende items hebt:

* Een geldige Azure-abonnement
* Een Cloud-Platform voor SAP HANA-account

Na het voltooien van deze zelfstudie, de Azure AD-gebruikers die u hebt toegewezen aan Cloud-Platform voor SAP HANA kan worden één Meld u aan bij de toepassing met behulp van de [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).

>[!IMPORTANT]
>U moet uw eigen toepassing implementeren of zich abonneert op een toepassing op uw Cloud-Platform voor SAP HANA-account voor het testen van eenmalige aanmelding op. In deze zelfstudie is een toepassing wordt geïmplementeerd in het account.
> 
> 

Het scenario in deze zelfstudie bestaat uit de volgende elementen:

1. De integratie van toepassingen voor SAP HANA Cloud-Platform inschakelen
2. Configureren van eenmalige aanmelding (SSO)
3. Een rol toewijst aan een gebruiker
4. Gebruikers toewijzen

![Scenario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scenario")

## <a name="enabling-the-application-integration-for-sap-hana-cloud-platform"></a>De integratie van toepassingen voor SAP HANA Cloud-Platform inschakelen
Het doel van deze sectie is het overzicht van de integratie van toepassingen voor SAP HANA Cloud-Platform inschakelen.

**Als u wilt de integratie van toepassingen voor SAP HANA Cloud-Platform inschakelen, moet u de volgende stappen uitvoeren:**

1. Klik in de Azure-beheerportal, in het navigatiedeelvenster links op **Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")
2. Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.
3. De weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.
   
    ![Toepassingen](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "toepassingen")
4. Klik op **toevoegen** aan de onderkant van de pagina.
   
    ![Toepassing toevoegen](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "toepassing toevoegen")
5. Op de **wat wilt u doen** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie**.
   
    ![Een toepassing toevoegen van gallerry](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "een toepassing van gallerry toevoegen")
6. In de **zoekvak**, type **SAP HANA-Cloudplatform**.
   
    ![Toepassingsgalerie](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "-Toepassingsgalerie")
7. Selecteer in het deelvenster met resultaten **SAP HANA-Cloudplatform**, en klik vervolgens op **Complete** de toepassing toevoegen.
   
    ![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")
   
## <a name="configure-single-sign-on"></a>Eenmalige aanmelding configureren

Het doel van deze sectie is om een overzicht van gebruikers te verifiëren en SAP HANA-Cloudplatform met hun account in Azure AD dat gebruikmaakt van Federatie op basis van het SAML-protocol in staat te.

Als onderdeel van deze procedure bent u een Base64-gecodeerde certificaat uploaden naar uw Cloud-Platform voor SAP HANA-tenant vereist.  

Als u niet bekend met deze procedure bent, raadpleegt u [het converteren van een binaire certificaat naar een tekstbestand](http://youtu.be/PlgrzUZ-Y1o)

**Voor het configureren van eenmalige aanmelding, moet u de volgende stappen uitvoeren:**

1. In de klassieke Azure-portal op de **SAP HANA-Cloudplatform** pagina van de integratie van toepassing, klikt u op **eenmalige aanmelding configureren** openen de **configureren eenmalige aanmelding** het dialoogvenster.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "eenmalige aanmelding configureren")
2. Op de **hoe wilt u dat gebruikers zich aanmelden op voor SAP HANA-Cloudplatform** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "eenmalige aanmelding configureren")
3. In een ander browservenster geopend, moet u zich aanmelden bij de SAP HANA Cloud Platform Cockpit op https://account. \<liggend host\>.ondemand.com/cockpit (bijvoorbeeld: *https://account.hanatrial.ondemand.com/cockpit*).
4. Klik op de **vertrouwen** tabblad.
   
    ![Vertrouwen](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "vertrouwen")
5. In de sectie trust management, kunt u de volgende stappen uitvoeren:
   
    ![Ophalen van metagegevens](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "metagegevens ophalen")
   
   1. Klik op de **lokale serviceprovider** tabblad.
   2. Voor het downloaden van het metagegevensbestand voor SAP HANA Cloud-Platform, klikt u op **metagegevens ophalen**.
6. In de Azure Active klassieke portal op de **App-URL configureren** pagina, voer de volgende stappen uit en klik vervolgens op **volgende**.
   
    ![App-URL configureren](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "App-URL configureren")
   
   1. In de **aanmelding op URL** textbox, typ de URL gebruikt door uw gebruikers zich aanmeldt bij uw **SAP HANA-Cloudplatform** toepassing. Dit is de account-specifieke URL van een beveiligde bron in uw Cloud-Platform voor SAP HANA-toepassing. De URL is gebaseerd op het volgende patroon volgen: *https://\<applicationName\>\<accountName\>.\< Liggend host\>.ondemand.com/\<pad\_naar\_beveiligd\_resource\>*  (bijvoorbeeld: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)
      
     >[!NOTE]
     >Dit is de URL in uw Cloud-Platform voor SAP HANA-toepassing waarvoor de gebruiker te verifiëren.
     > 

   2. Open het gedownloade bestand van de Cloud-Platform voor SAP HANA-metagegevens, en Ga naar de **ns3:AssertionConsumerService** label.
   3. Kopieer de waarde van de **locatie** kenmerk en plak deze in de **antwoord-URL voor SAP HANA Cloud Platform** textbox.

7. Op de **eenmalige aanmelding configureren op SAP HANA-Cloudplatform** pagina voor het downloaden van de metagegevens, klikt u op **metagegevens downloaden**, en sla het bestand op uw computer.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "eenmalige aanmelding configureren")
8. Op de Cockpit SAP HANA Cloud Platform in de **lokale serviceprovider** sectie, voert u de volgende stappen uit:
   
    ![Beheer vertrouwen](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "beheer vertrouwen")
   
  1. Klik op **Bewerken**.
  2. Als **configuratietype**, selecteer **aangepaste**.
  3. Als **lokale providernaam**, accepteer de standaardwaarde.
  4. Voor het genereren van een **handtekeningsleutel** en een **certificaat voor ondertekening van** sleutelpaar, klikt u op **sleutelpaar genereren**.
  5. Als **Principal doorgeven**, selecteer **uitgeschakelde**.
  6. Als **Force verificatie**, selecteer **uitgeschakelde**.
  7. Klik op **Opslaan**.

9. Klik op de **identiteitsprovider vertrouwde** tabblad en klik vervolgens op **vertrouwde identiteitsprovider toevoegen**.
   
    ![Beheer vertrouwen](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "beheer vertrouwen")
   
    >[!NOTE]
    >Voor het beheren van de lijst met vertrouwde id-providers, moet u het type aangepaste configuratie hebt gekozen in de sectie lokale-Provider. U hebt een niet-bewerkbare en impliciete vertrouwensrelatie met de SAP-id-Service voor het type standaard configuratie. Voor geen hebt u geen vertrouwensrelatie instellingen.
    > 
    > 

10. Klik op de **algemene** tabblad en klik vervolgens op **Bladeren** het gedownloade metagegevensbestand te uploaden.
    
    ![Beheer vertrouwen](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "beheer vertrouwen")
    
    >[!NOTE]
    >Na het uploaden van het metagegevensbestand, de waarden voor **-URL met eenmalige aanmelding**, **-URL met eenmalige afmelding** en **certificaat voor ondertekening van** worden automatisch ingevuld.
    > 
    > 

11. Klik op het tabblad **Kenmerken**.
12. Op de **kenmerken** tabblad, voert u de volgende stap:
    
    ![Kenmerken](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "kenmerken") 
  * Klik op **Add Assertion-Based kenmerk**, en voeg vervolgens de volgende kenmerken op basis van een bevestiging:
       
    | Verklaring kenmerk | Principal-kenmerk |
    | --- | --- |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/givenName |Voornaam |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/surname |Achternaam |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/EmailAddress |E-mail 
   
     >[!NOTE]
     >De configuratie van de kenmerken is afhankelijk van hoe de toepassingen op de rechtermuisknop worden ontwikkeld, dat wil zeggen welke kenmerken ze in de SAML-reactie verwachten en onder welke naam (Principal kenmerk) toegang tot dit kenmerk in de code.
     > 
     >  

    1.  De **kenmerk Default** in de schermafbeelding is alleen bedoeld ter illustratie. Het is niet vereist voor het maken van het scenario werken.   
    2.  De namen en waarden voor **Principal kenmerk** weergegeven in de schermafbeelding afhankelijk van hoe de toepassing is ontwikkeld. Het is mogelijk dat uw toepassing andere toewijzingen vereist.
     
13. In de klassieke Azure-portal op de **eenmalige aanmelding configureren op SAP HANA-Cloudplatform** dialoog pagina, selecteert u de configuratie voor één aanmelding bevestiging en klik vervolgens op **Complete**.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "eenmalige aanmelding configureren")

###<a name="assertion-based-groups"></a>Verklaring gebaseerde groepen
U kunt groepen op basis van een bevestiging voor uw Azure Active Directory id-Provider configureren als een optionele stap.

Met behulp van groepen op SAP HANA Cloud-Platform, kunt u een of meer gebruikers dynamisch toewijzen aan een of meer rollen in uw Cloud-Platform voor SAP HANA-toepassingen, bepaald door de waarden van kenmerken in het SAML 2.0-verklaring. 

Bijvoorbeeld, als de bevestiging bevat het kenmerk '*contract = tijdelijke*', kunt u alle betrokken gebruikers worden toegevoegd aan de groep'*tijdelijke*'. De groep '*tijdelijke*' een of meer rollen van een of meer toepassingen die zijn geïmplementeerd in uw Cloud-Platform voor SAP HANA-account kan bevatten.
 
Groepen op basis van een bewering gebruiken wanneer u veel gebruikers tegelijk toewijzen aan een of meer rollen van toepassingen in uw Cloud-Platform voor SAP HANA-account wilt maken. Als u toewijzen slechts een enkele of een klein aantal gebruikers aan specifieke rollen wilt, raden wij aan eraan toe te wijzen rechtstreeks in de '**autorisaties**' tabblad van de cockpit SAP HANA Cloud-Platform.

## <a name="assign-a-role-to-a-user"></a>Een rol toewijzen aan een gebruiker
Om in te schakelen gebruikers van Azure AD aan te melden bij SAP HANA Cloud-Platform, moet u rollen in de Cloud Platform voor SAP HANA aan ze toewijzen.

**Als u wilt een rol toewijzen aan een gebruiker, moet u de volgende stappen uitvoeren:**

1. Meld u aan bij uw **SAP HANA-Cloudplatform** cockpit.
2. Het volgende doen:
   
   ![Autorisaties](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "autorisaties")
   
  1. Klik op **autorisatie**.
  2. Klik op de **gebruikers** tabblad.
  3. In de **gebruiker** textbox, typ de e-mailadres van de gebruiker.
  4. Klik op **toewijzen** toewijzen aan de gebruiker aan een rol.
  5. Klik op **Opslaan**.

## <a name="assign-users"></a>Gebruikers toewijzen
Als u wilt testen van uw configuratie, moet u de Azure AD-gebruikers verlenen die u wilt toestaan dat met behulp van uw toepassing toegang tot deze door toe te wijzen.

**Gebruikers om aan te wijzen SAP HANA Cloud-Platform, moet u de volgende stappen uitvoeren:**

1. In de klassieke Azure portal een testaccount te maken.
2. Op de **SAP HANA-Cloudplatform** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.
   
   ![Gebruikers toewijzen](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "gebruikers toewijzen")
3. Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** om te bevestigen dat de toewijzing.
   
   ![Ja](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Ja")

Als u testen van uw instellingen voor eenmalige aanmelding wilt, opent u het toegangsvenster. Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).

