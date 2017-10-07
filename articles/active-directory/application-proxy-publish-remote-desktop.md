---
title: aaaPublish extern bureaublad met Azure AD-toepassingsproxy | Microsoft Docs
description: Bevat informatie over Hallo basisbeginselen van Azure AD-toepassingsproxy connectors.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: kgremban
ms.custom: it-pro
ms.reviewer: harshja
ms.openlocfilehash: 1174161d0b5ef1157c334970f00ef4f0702a9545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-remote-desktop-with-azure-ad-application-proxy"></a>Extern bureaublad met Azure AD-toepassingsproxy publiceren

In dit artikel bevat informatie over hoe toodeploy Remote Desktop Services (RDS) met toepassingsproxy zodat externe gebruikers nog steeds productief kunnen zijn.

Hallo bedoeld is bedoeld voor dit artikel:
- Huidige Azure AD-toepassingsproxy-klanten die toooffer meer toepassingen tootheir-eindgebruikers willen door het publiceren van on-premises toepassingen via Extern bureaublad-Services.
- Huidige extern bureaublad-Services voor klanten die tooreduce Hallo kwetsbaarheid voor aanvallen van hun implementatie willen met behulp van Azure AD-toepassingsproxy. Dit scenario biedt een beperkte set van verificatie in twee stappen en voorwaardelijke toegang tooRDS beheert.

## <a name="how-application-proxy-fits-in-hello-standard-rds-deployment"></a>Hoe Application Proxy past in Hallo RDS-implementatie

Een standaardimplementatie van RDS bevat verschillende functieservices van extern bureaublad met Windows Server. Bekijkt hello [extern bureaublad-Services architectuur](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture), er zijn meerdere implementatie-opties. meest merkbaar verschil tussen Hallo Hallo [RDS-implementatie met Azure AD-toepassingsproxy](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture) (weergegeven in het volgende diagram Hallo) en hello andere implementatie-opties is Hallo toepassingsproxy in dit scenario is een permanente uitgaand de verbinding van Hallo server Hallo-connectorservice wordt uitgevoerd. Andere implementaties laat open binnenkomende verbindingen via een load balancer.

![Een toepassing Proxy zich tussen Hallo RDS VM en Hallo openbare internet](./media/application-proxy-publish-remote-desktop/rds-with-app-proxy.png)

In een RDS-implementatie Hallo extern bureaublad-Webrol en Hallo RD-Gateway rol worden uitgevoerd op Internet gerichte machines. Deze eindpunten beschikbaar worden gesteld voor Hallo volgende redenen:
- RD Web biedt Hallo gebruiker een openbaar eindpunt toosign in en weergave Hallo verschillende on-premises toepassingen en bureaubladen toegang te krijgen tot. Een RDP-verbinding wordt gemaakt via de systeemeigen app Hallo op Hallo OS bij het selecteren van een resource.
- RD-Gateway wordt geleverd in Hallo afbeelding zodra een gebruiker Hallo RDP-verbinding start. Hallo RD-Gateway Hallo versleuteld RDP-verkeer binnenkomt via Internet Hallo verwerkt en zet deze lokale server die Hallo gebruiker verbinding met maakt toohello. In dit scenario is Hallo verkeer Hallo die RD-Gateway ontvangt afkomstig van hello Azure AD-toepassingsproxy.

>[!TIP]
>Als u RDS voordat u dit nog niet hebt geïmplementeerd, of u meer informatie wilt voordat u begint, informatie over hoe te[naadloos implementeren RDS met Azure Resource Manager en Azure Marketplace](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure).

## <a name="requirements"></a>Vereisten

- Beide RD Web Hallo en RD-Gateway eindpunten moeten zich bevinden op dezelfde computer, en met een algemene basis Hallo. RD Web- en RD-Gateway zal worden gepubliceerd als één toepassing zodat u kunt een ervaring voor eenmalige aanmelding tussen Hallo twee toepassingen hebt.

- U hebt al [geïmplementeerd RDS](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure), en [toepassingsproxy hebt ingeschakeld](active-directory-application-proxy-enable.md).

- Dit scenario veronderstelt dat uw eindgebruikers gaan via Internet Explorer op Windows 7 of Windows 10-desktops die verbinding via Extern bureaublad-webpagina Hallo maken. Als u toosupport andere besturingssystemen moet, Zie [ondersteuning voor andere clientconfiguraties](#support-for-other-client-configurations).

  >[!NOTE]
  >Update voor Windows 10 Creator is momenteel niet ondersteund.

- Schakel Hallo RDS ActiveX-invoegtoepassing op Internet Explorer.

## <a name="deploy-hello-joint-rds-and-application-proxy-scenario"></a>Hallo gezamenlijke RDS en toepassingsproxy scenario implementeren

Volg na het instellen van RDS en Azure AD-toepassingsproxy voor uw omgeving, Hallo stappen toocombine Hallo twee oplossingen. Deze stappen doorlopen die Hallo web gerichte RDS eindpunten (RD Web en RD-Gateway) publiceren als toepassingen, en vervolgens het routeren van verkeer op uw toogo RDS via toepassingsproxy.

### <a name="publish-hello-rd-host-endpoint"></a>Hallo RD host eindpunt publiceren

1. [Een nieuwe Application Proxy-toepassing publiceren](application-proxy-publish-azure-portal.md) Hello volgende waarden:
   - Interne URL: https://\<rdhost\>.com / waar \<rdhost\> Hallo algemene hoofdmap die RD Web- en RD-Gateway delen.
   - Externe URL: Dit veld wordt automatisch ingevuld op basis van Hallo-naam van de toepassing hello, maar u kunt deze wijzigen. Uw gebruikers gaat toothis URL wanneer ze toegang krijgen RDS. tot
   - Methode voor verificatie vooraf: Azure Active Directory
   - URL-headers vertalen: Nee
2. Gebruikers toewijzen toohello gepubliceerd extern bureaublad-toepassing. Zorg ervoor dat ze alle access-tooRDS te hebben.
3. Hallo één aanmelding methode voor de toepassing hello als laat **Azure AD eenmalige aanmelding uitgeschakeld**. Uw gebruikers worden gevraagd tooauthenticate zodra tooAzure AD en eens tooRD Web, maar één aanmelding tooRD Gateway hebt.
4. Ga te**Azure Active Directory** > **App registraties** > *uw toepassing* > **instellingen**.
5. Selecteer **eigenschappen** en update Hallo **start-pagina-URL** veld toopoint tooyour RD Web-eindpunt (zoals https://\<rdhost\>.com/RDWeb).

### <a name="direct-rds-traffic-tooapplication-proxy"></a>Directe RDS verkeer tooApplication Proxy

Verbind toohello RDS-implementatie als beheerder en Hallo RD-Gateway-servernaam voor de implementatie van Hallo wijzigen. Dit zorgt ervoor dat verbindingen hello Azure AD-toepassingsproxy doorlopen.

1. Verbinding maken met toohello RDS-server met Hallo RD Connection Broker-functie.
2. Start **Serverbeheer**.
3. Selecteer **extern bureaublad-Services** in Hallo deelvenster op Hallo links.
4. Selecteer **overzicht**.
5. Selecteer de vervolgkeuzelijst Hallo in Hallo sectie overzicht van de implementatie, en kies **implementatie-eigenschappen bewerken**.
6. Hallo RD-Gateway tabblad wijzigen Hallo **servernaam** veld toohello externe URL die u voor extern bureaublad Hallo host eindpunt in Application Proxy instelt.
7. Wijziging Hallo **aanmelden methode** veld te**wachtwoordverificatie**.

  ![Scherm van de eigenschappen van implementatie van RDS](./media/application-proxy-publish-remote-desktop/rds-deployment-properties.png)

8. Voor elke verzameling Hallo volgende opdracht worden uitgevoerd. Vervang  *\<yourcollectionname\>*  en  *\<proxyfrontendurl\>*  met uw eigen gegevens. Met deze opdracht kunt eenmalige aanmelding tussen RD Web- en RD-Gateway en optimaliseert de prestaties:

   ```
   Set-RDSessionCollectionConfiguration -CollectionName "<yourcollectionname>" -CustomRdpProperty "pre-authentication server address:s:<proxyfrontendurl>`nrequire pre-authentication:i:1"
   ```

   **Bijvoorbeeld:**
   ```
   Set-RDSessionCollectionConfiguration -CollectionName "QuickSessionCollection" -CustomRdpProperty "pre-authentication server address:s:https://gateway.contoso.msappproxy.net/`nrequire pre-authentication:i:1"
   ```

9. tooverify hello wijziging van Hallo aangepaste RDP-eigenschappen, evenals Hallo RDP-bestandsinhoud weergeven die worden gedownload vanaf RDWeb voor deze verzameling, Hallo volgende opdracht uitvoeren:
    ```
    (get-wmiobject -Namespace root\cimv2\terminalservices -Class Win32_RDCentralPublishedRemoteDesktop).RDPFileContents
    ```

Nu dat u hebt geconfigureerd dat extern bureaublad, is Azure AD-toepassingsproxy overgenomen als onderdeel van het internet gerichte Hallo van RDS. U kunt verwijderen Hallo andere openbare internetgerichte eindpunten op uw extern bureaublad-Web- en RD-Gateway-machines.

## <a name="test-hello-scenario"></a>Hallo Testscenario

Hallo-scenario met Internet Explorer op een Windows 7 of 10 computer testen.

1. Ga toohello externe URL die u instelt of uw toepassing niet vinden in Hallo [MyApps Configuratiescherm](https://myapps.microsoft.com).
2. U wordt gevraagd tooauthenticate tooAzure Active Directory. Gebruik een account dat u de toepassing toohello toegewezen.
3. U wordt gevraagd tooauthenticate tooRD Web.
4. Zodra de RDS-verificatie is gelukt, kunt u Hallo bureaublad of toepassing die u wilt en aan de slag.

## <a name="support-for-other-client-configurations"></a>Ondersteuning voor andere clientconfiguraties

Hallo-configuratie zoals beschreven in dit artikel is bedoeld voor gebruikers in Windows 7 of 10, met Internet Explorer, plus Hallo RDS ActiveX-invoegtoepassing. Als u wilt echter, kunt u ondersteuning voor andere besturingssystemen of browsers. Hallo verschil is Hallo verificatiemethode die u gebruikt.

| Verificatiemethode | Ondersteunde client-configuratie |
| --------------------- | ------------------------------ |
| Verificatie vooraf    | Windows 7/10 met behulp van Internet Explorer + RDS ActiveX-invoegtoepassing |
| Passthrough | Een ander besturingssysteem die ondersteuning biedt voor de Microsoft Extern bureaublad-toepassing hello |

Hallo vooraf-authenticatiestroom biedt de voordelen van meer beveiliging dan Hallo passthrough-stroom. Met verificatie vooraf kunt u gebruikmaken van Azure AD authenticatiefuncties zoals het eenmalige aanmelding, voorwaardelijke toegang en verificatie in twee stappen voor uw lokale resources. U ook voor zorgen dat alleen geverifieerd verkeer bereikt uw netwerk.

toouse passthrough-verificatie, er slechts twee wijzigingen toohello stappen worden vermeld in dit artikel:
1. In [publiceren Hallo RD host eindpunt](#publish-the-rd-host-endpoint) stap 1, stelt u de methode voor verificatie vooraf hello te**Passthrough**.
2. In [Direct RDS verkeer tooApplication Proxy](#direct-rds-traffic-to-application-proxy), slaat u stap 8 volledig.

## <a name="next-steps"></a>Volgende stappen

[Externe toegang tooSharePoint met Azure AD-toepassingsproxy inschakelen](application-proxy-enable-remote-access-sharepoint.md)  
[Beveiligingsoverwegingen voor toegang tot de apps op afstand met behulp van Azure AD-toepassingsproxy](application-proxy-security-considerations.md)
