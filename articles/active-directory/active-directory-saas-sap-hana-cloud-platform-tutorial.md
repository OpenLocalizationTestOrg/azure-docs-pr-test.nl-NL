---
title: 'Zelfstudie: Azure Active Directory-integratie met SAP HANA-Cloudplatform | Microsoft Docs'
description: Lees hoe toouse SAP HANA-Cloudplatform met Azure Active Directory tooenable eenmalige aanmelding, geautomatiseerde inrichting en meer.
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
ms.openlocfilehash: cc6610969b1c7b08f776e6969a5977fc75eb9ab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a>Zelfstudie: Azure Active Directory-integratie met SAP HANA-cloudplatform
Hallo-doel van deze zelfstudie is tooshow Hallo integratie van Azure en SAP HANA-Cloud-Platform.

Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:

* Een geldige Azure-abonnement
* Een Cloud-Platform voor SAP HANA-account

Na het voltooien van deze zelfstudie hello Azure AD-gebruikers die u hebt tooSAP HANA Cloud-Platform worden kunnen toosingle aanmelding toegewezen aan Hallo toepassing hello [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

>[!IMPORTANT]
>U moet toodeploy uw eigen toepassing of tooan toepassing abonneren op uw SAP HANA Cloud Platform account tootest eenmalige aanmelding. In deze zelfstudie is een toepassing wordt geïmplementeerd in Hallo-account.
> 
> 

Hallo scenario beschreven in deze zelfstudie bestaat uit Hallo bouwstenen te volgen:

1. Hallo toepassingsintegratie voor SAP HANA Cloud-Platform inschakelen
2. Configureren van eenmalige aanmelding (SSO)
3. Een rol tooa gebruiker toewijzen
4. Gebruikers toewijzen

![Scenario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scenario")

## <a name="enabling-hello-application-integration-for-sap-hana-cloud-platform"></a>Hallo toepassingsintegratie voor SAP HANA Cloud-Platform inschakelen
Hallo-doel van deze sectie is het toooutline hoe tooenable Hallo toepassingsintegratie voor SAP HANA Cloud-Platform.

**tooenable hello toepassingsintegratie voor SAP HANA Cloud Platform Hallo stappen uitvoeren:**

1. Klik in hello Azure-beheerportal op Hallo navigatiedeelvenster links op **Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")
2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.
3. tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.
   
    ![Toepassingen](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "toepassingen")
4. Klik op **toevoegen** Hallo Hallo pagina onderaan in.
   
    ![Toepassing toevoegen](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "toepassing toevoegen")
5. Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.
   
    ![Een toepassing toevoegen van gallerry](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "een toepassing van gallerry toevoegen")
6. In Hallo **zoekvak**, type **SAP HANA-Cloudplatform**.
   
    ![Toepassingsgalerie](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "-Toepassingsgalerie")
7. Selecteer in het deelvenster met resultaten Hallo **SAP HANA-Cloudplatform**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.
   
    ![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")
   
## <a name="configure-single-sign-on"></a>Eenmalige aanmelding configureren

Hallo-doel van deze sectie is toooutline hoe tooenable gebruikers tooauthenticate tooSAP HANA Cloudplatform met een account in Azure AD dat gebruikmaakt van Federatie gebaseerd op Hallo SAML-protocol.

Als onderdeel van deze procedure bent u vereiste tooupload een Base64-gecodeerde certificaat tooyour Cloudplatform voor SAP HANA-tenant.  

Als u niet bekend met deze procedure bent, raadpleegt u [hoe tooconvert een binair bestand van het certificaat naar een tekstbestand](http://youtu.be/PlgrzUZ-Y1o)

**tooconfigure eenmalige aanmelding, voert u Hallo stappen te volgen:**

1. In de klassieke Azure-portal op Hallo Hallo **SAP HANA-Cloudplatform** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren eenmalige aanmelding**dialoogvenster.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "eenmalige aanmelding configureren")
2. Op Hallo **wilt u hoe gebruikers toosign op tooSAP HANA Cloudplatform** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "eenmalige aanmelding configureren")
3. Een ander browservenster, meld u aan bij toohello SAP HANA Cloud Platform Cockpit op https://account. \<liggend host\>.ondemand.com/cockpit (bijvoorbeeld: *https://account.hanatrial.ondemand.com/cockpit*).
4. Klik op Hallo **vertrouwen** tabblad.
   
    ![Vertrouwen](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "vertrouwen")
5. In de sectie voor het beheren van vertrouwensrelatie uitvoeren Hallo stappen te volgen:
   
    ![Ophalen van metagegevens](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "metagegevens ophalen")
   
   1. Klik op Hallo **lokale serviceprovider** tabblad.
   2. toodownload hello metagegevensbestand voor SAP HANA Cloud-Platform, klikt u op **metagegevens ophalen**.
6. In hello Azure Active klassieke portal op Hallo **App-URL configureren** pagina, het uitvoeren van Hallo volgende stappen uit en klik vervolgens op **volgende**.
   
    ![App-URL configureren](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "App-URL configureren")
   
   1. In Hallo **aanmelding op URL** textbox type Hallo-URL die wordt gebruikt door uw toosign gebruikers in uw **SAP HANA-Cloudplatform** toepassing. Dit is Hallo accountspecifiek URL van een beveiligde bron in uw Cloud-Platform voor SAP HANA-toepassing. Hallo URL is op basis van Hallo patroon volgen: *https://\<applicationName\>\<accountName\>.\< Liggend host\>.ondemand.com/\<pad\_naar\_beveiligd\_resource\>*  (bijvoorbeeld: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)
      
     >[!NOTE]
     >Dit is de URL Hallo in uw Cloud-Platform voor SAP HANA-toepassing die Hallo gebruiker tooauthenticate vereist.
     > 

   2. Open metagegevensbestand voor SAP HANA-Cloudplatform Hallo gedownload, en Ga naar Hallo **ns3:AssertionConsumerService** label.
   3. Kopieer de waarde Hallo Hallo **locatie** kenmerk en plak deze in Hallo **antwoord-URL voor SAP HANA Cloud Platform** textbox.

7. Op Hallo **eenmalige aanmelding configureren op SAP HANA-Cloudplatform** pagina, toodownload uw metagegevens, klikt u op **metagegevens downloaden**, en sla Hallo-bestand op uw computer.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "eenmalige aanmelding configureren")
8. Op Hallo SAP HANA Cloud Platform Cockpit in Hallo **lokale serviceprovider** sectie, voert u Hallo stappen te volgen:
   
    ![Beheer vertrouwen](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "beheer vertrouwen")
   
  1. Klik op **Bewerken**.
  2. Als **configuratietype**, selecteer **aangepaste**.
  3. Als **lokale providernaam**, accepteer de standaardwaarde Hallo.
  4. toogenerate een **handtekeningsleutel** en een **certificaat voor ondertekening van** sleutelpaar, klikt u op **sleutelpaar genereren**.
  5. Als **Principal doorgeven**, selecteer **uitgeschakelde**.
  6. Als **Force verificatie**, selecteer **uitgeschakelde**.
  7. Klik op **Opslaan**.

9. Klik op Hallo **identiteitsprovider vertrouwde** tabblad en klik vervolgens op **vertrouwde identiteitsprovider toevoegen**.
   
    ![Beheer vertrouwen](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "beheer vertrouwen")
   
    >[!NOTE]
    >toomanage hello lijst met vertrouwde id-providers, moet u toohave Hallo aangepaste configuratietype in Hallo lokale serviceprovider sectie gekozen. U hebt een niet-bewerkbare en impliciete vertrouwensrelatie toohello SAP-id-Service voor het type standaard configuratie. Voor geen hebt u geen vertrouwensrelatie instellingen.
    > 
    > 

10. Klik op Hallo **algemene** tabblad en klik vervolgens op **Bladeren** tooupload Hallo gedownload bestand met metagegevens.
    
    ![Beheer vertrouwen](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "beheer vertrouwen")
    
    >[!NOTE]
    >Na het uploaden van het metagegevensbestand Hallo Hallo waarden voor **-URL met eenmalige aanmelding**, **-URL met eenmalige afmelding** en **certificaat voor ondertekening van** worden automatisch ingevuld.
    > 
    > 

11. Klik op Hallo **kenmerken** tabblad.
12. Op Hallo **kenmerken** tabblad, voert u Hallo stap:
    
    ![Kenmerken](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "kenmerken") 
  * Klik op **Add Assertion-Based kenmerk**, en voeg vervolgens Hallo kenmerken op basis van een verklaring te volgen:
       
    | Verklaring kenmerk | Principal-kenmerk |
    | --- | --- |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/givenName |Voornaam |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/surname |Achternaam |
    | http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/EmailAddress |E-mail 
   
     >[!NOTE]
     >Hallo-configuratie van Hallo kenmerken is afhankelijk van de hoe Hallo toepassing(en) op rechtermuisknop worden ontwikkeld, dat wil zeggen welke kenmerken ze verwachten in Hallo SAML-reactie en onder welke naam (Principal kenmerk) toegang tot dit kenmerk in het Hallo-code.
     > 
     >  

    1.  Hallo **kenmerk Default** in Hallo schermafbeelding is alleen ter illustratie. Het is niet toomake Hallo scenario werk vereist.   
    2.  Hallo namen en waarden voor **Principal kenmerk** wordt weergegeven in Hallo schermafbeelding is afhankelijk van hoe de toepassing hello is ontwikkeld. Het is mogelijk dat uw toepassing andere toewijzingen vereist.
     
13. In de klassieke Azure-portal op Hallo Hallo **eenmalige aanmelding configureren op SAP HANA-Cloudplatform** dialoog pagina, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik op **Complete**.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "eenmalige aanmelding configureren")

###<a name="assertion-based-groups"></a>Verklaring gebaseerde groepen
U kunt groepen op basis van een bevestiging voor uw Azure Active Directory id-Provider configureren als een optionele stap.

Groepen gebruiken voor SAP HANA Cloud Platform kunt u toodynamically toewijzen een of meer gebruikers tooone of meer functies in uw toepassingen SAP HANA-Cloudplatform bepaald door waarden van kenmerken in Hallo SAML 2.0-verklaring. 

Bijvoorbeeld, als hello assertion bevat Hallo kenmerk '*contract = tijdelijke*', kunt u alle betrokken gebruikers toobe toegevoegde toohello groep'*tijdelijke*'. Hallo groep '*tijdelijke*' een of meer rollen van een of meer toepassingen die zijn geïmplementeerd in uw Cloud-Platform voor SAP HANA-account kan bevatten.
 
Gebruik assertion gebaseerde groepen als u wilt dat toosimultaneously toewijzen veel gebruikers tooone of meer functies van toepassingen in uw Cloud-Platform voor SAP HANA-account. Als u wilt dat tooassign slechts een enkele of een klein aantal gebruikers toospecific rollen, raden wij aan eraan toe te wijzen rechtstreeks in Hallo '**autorisaties**' hello SAP HANA-Cloudplatform cockpit tabblad.

## <a name="assign-a-role-tooa-user"></a>Een rol tooa gebruiker toewijzen
In de volgorde tooenable Azure AD gebruikers toolog in SAP HANA Cloud-Platform, moet u de rollen in Hallo SAP HANA-Cloudplatform toothem toewijzen.

**tooassign een rol tooa gebruiker, voert u Hallo stappen te volgen:**

1. Meld u bij tooyour **SAP HANA-Cloudplatform** cockpit.
2. Voer de volgende Hallo:
   
   ![Autorisaties](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "autorisaties")
   
  1. Klik op **autorisatie**.
  2. Klik op Hallo **gebruikers** tabblad.
  3. In Hallo **gebruiker** textbox e-mailadres type Hallo gebruiker.
  4. Klik op **toewijzen** tooassign hello tooa gebruikersrol.
  5. Klik op **Opslaan**.

## <a name="assign-users"></a>Gebruikers toewijzen
tootest uw configuratie, moet u toogrant hello Azure AD-gebruikers gewenste tooallow met behulp van uw toepassing toegang tooit door toe te wijzen.

**tooassign gebruikers tooSAP HANA Cloud-Platform, Voer Hallo stappen te volgen:**

1. In de klassieke Azure-portal hello, een testaccount te maken.
2. Op Hallo **SAP HANA-Cloudplatform** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.
   
   ![Gebruikers toewijzen](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "gebruikers toewijzen")
3. Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** tooconfirm de toewijzing.
   
   ![Ja](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Ja")

Als u uw instellingen SSO tootest wilt, open Hallo Toegangsvenster. Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

