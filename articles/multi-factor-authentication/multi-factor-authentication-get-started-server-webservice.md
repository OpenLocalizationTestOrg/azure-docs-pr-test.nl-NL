---
title: Webservice voor mobiele Apps voor MFA-Server aaaAzure | Microsoft Docs
description: Hallo Microsoft Authenticator-app biedt een extra out-of-band-verificatie-optie.  Kunt u MFA server toouse push notifications toousers Hallo.
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 6c8d6fcc-70f4-4da4-9610-c76d66635b8b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 4175b68fcbf85ec3fd53d8edf4e07306c75a4c71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-mobile-app-authentication-with-azure-multi-factor-authentication-server"></a>Authenticatie met de mobiele app integreren met Azure Multi-Factor Authentication-server

Hallo Microsoft Authenticator-app biedt een aanvullende verificatie voor out-of-band-optie. In plaats van een automatisch telefoongesprek of SMS toohello gebruiker tijdens het aanmelden, stuurt Azure multi-factor Authentication een melding toohello Microsoft Authenticator-app op de smartphone of tablet Hallo van de gebruiker. Hallo gebruiker gewoon op tikt **controleren** (of een PINCODE invoert en op 'Verifiëren' tikt) Hallo in app toocomplete hun aanmelden.

Het gebruik van een mobiele app voor verificatie in twee stappen wordt aanbevolen wanneer het telefonische bereik onbetrouwbaar is. Als u Hallo-app als een OATH-token generator, nodig niet het netwerk of internet-verbinding.

Afhankelijk van uw omgeving, kunt u toodeploy Hallo mobiele app-webservice op Hallo dezelfde server als de Azure multi-factor Authentication-Server of op een andere internetgerichte server.

## <a name="requirements"></a>Vereisten

toouse hello Microsoft Authenticator-app Hallo volgende is vereist zodat hello app correct te laten met de webservice voor mobiele App communiceren:

* Azure Multi-Factor Authentication-server versie 6.0 of hoger.
* De webservice voor mobiele apps moet zijn geïnstalleerd op een internetgerichte webserver waarop Microsoft® [Internet Information Services (IIS) 7.x of hoger](http://www.iis.net/) wordt uitgevoerd.
* ASP.NET v4.0.30319 is geïnstalleerd, is geregistreerd en tooAllowed instellen
* Vereiste functieservices omvatten ASP.NET en compatibiliteit met IIS 6-metabase.
* Webservice voor mobiele apps moet toegankelijk zijn via een openbare URL.
* Webservice voor mobiele apps moet met een SSL-certificaat zijn beveiligd.
* Hello Azure multi-factor Authentication Web Service SDK installeren in IIS 7.x of hoger op Hallo **dezelfde server als hello Azure multi-factor Authentication-Server**
* Hello Azure multi-factor Authentication Web Service SDK is beveiligd met een SSL-certificaat.
* Webservice voor mobiele App verbinding kunnen maken van Azure multi-factor Authentication Web Service SDK toohello via SSL
* Webservice voor mobiele App toohello Azure MFA Web Service SDK kan worden geverifieerd met behulp van referenties van een serviceaccount dat lid is van de beveiligingsgroep voor Hallo "PhoneFactor Admins" Hallo. Dit serviceaccount en deze groep bevinden zich in Active Directory als hello Azure multi-factor Authentication-Server zich op een domein-server. Dit serviceaccount en deze groep bevinden zich lokaal op Hallo Azure multi-factor Authentication-Server als geen gekoppelde tooa-domein is.

## <a name="install-hello-mobile-app-web-service"></a>Hallo mobiele app-webservice installeren

Voordat u Hallo mobiele app webservice installeert, worden op de hoogte van Hallo volgende details:

* U moet een serviceaccount hebben dat deel uitmaakt van de groep 'PhoneFactor Admins'. Dit account kan hetzelfde als een Hallo voor de installatie van de Gebruikersportal Hallo gebruikt Hallo worden.
* Het is nuttig tooopen een webbrowser op Hallo internetgerichte webserver en toohello-URL van webservice-SDK die is ingevoerd in het web.config-bestand Hallo Hallo navigeren. Als Hallo browser kunt u toohello-webservice is, moet dit om referenties gevraagd. Voer Hallo gebruikersnaam en wachtwoord zijn ingevoerd Hallo web.config-bestand exact in zoals deze wordt weergegeven in het Hallo-bestand. Controleer of er geen certificaatwaarschuwingen of -fouten worden weergegeven.
* Als een omgekeerde proxy of firewall zit Hallo webservice voor mobiele App-webserver en uitvoeren van SSL-offloading, kunt u Hallo webservice voor mobiele App web.config-bestand bewerken zodat hello webservice voor mobiele Apps http in plaats van https gebruiken kan. SSL is nog steeds vereist vanuit Hallo mobiele App toohello firewall/omgekeerde proxy. Hallo sleutel toohello na toevoegen \<appSettings\> sectie:

        <add key="SSL_REQUIRED" value="false"/>

### <a name="install-hello-web-service-sdk"></a>Hallo webservice SDK installeren

In beide scenario's moet hello Azure multi-factor Authentication Web Service SDK is **niet** op Hallo Azure multi-factor Authentication (MFA)-Server zijn geïnstalleerd, volledige Hallo onderstaande stappen.

1. Open de console van Hallo multi-factor Authentication-Server.
2. Ga toohello **Web Service SDK** en selecteer **Web Service SDK installeren**.
3. Volledige Hallo installeren met behulp van Hallo standaardwaarden tenzij u toochange hoeft ze om een bepaalde reden.
4. Binden van een SSL-certificaat toohello-website in IIS.

Als u vragen over het configureren van een SSL-certificaat op een IIS-server hebt, raadpleegt u Hallo artikel [hoe tooSet SSL op IIS](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

Hallo Web Service SDK moet worden beveiligd met een SSL-certificaat. Voor dit doel kan een zelfondertekend certificaat worden gebruikt. Hallo-certificaat importeren in Hallo 'Trusted Root Certification Authorities' archief van de lokale computeraccount Hallo op Hallo User Portal-webserver, zodat wordt dat certificaat vertrouwd wanneer Hallo SSL-verbinding tot stand brengen.

![Configuratie van MFA-server - webservice-SDK installeren](./media/multi-factor-authentication-get-started-server-webservice/sdk.png)

### <a name="install-hello-service"></a>Hallo-service installeren

1. **Op Hallo MFA-Server**, toohello installatiepad bladeren.
2. Navigeer toohello map waar hello Azure MFA-Server standaard geïnstalleerd Hallo is is **C:\Program Files\Azure multi-factor Authentication**.
3. Zoek het installatiebestand Hallo **MultiFactorAuthenticationMobileAppWebServiceSetup64**. Als de server Hallo **niet** internetgerichte, kopie Hallo installatie bestand toohello internetgerichte server.
4. Als hello MFA-Server is **niet** internetgerichte switch toohello **internetgerichte server**.
5. Voer Hallo **MultiFactorAuthenticationMobileAppWebServiceSetup64** bestand installeren als een beheerder, Hallo Site desgewenst wijzigen en Hallo virtuele directory tooa korte naam wijzigen als u wilt.
6. Na de einddatum Hallo-installatie te bladeren**C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService** (of de juiste map op basis van de naam van de virtuele map Hallo) en bewerk Hallo Web.Config-bestand.

   * Hallo sleutel vinden **'Sleutels WEB_SERVICE_SDK_AUTHENTICATION_USERNAME'** en wijzig **waarde = ""** te**waarde = 'Domein\gebruiker'** waar domein\gebruiker is een Service-Account dat deel uitmaakt van 'PhoneFactor Admins'-groep.
   * Hallo sleutel vinden **'WEB_SERVICE_SDK_AUTHENTICATION_PASSWORD'** en wijzig **waarde = ""** te**waarde = 'Password'** waar het wachtwoord is Hallo-wachtwoord voor Hallo Service Het account is ingevoerd in de vorige regel Hallo.
   * Hallo zoeken **instelling pfMobile App Web Service_pfwssdk_PfWsSdk** instellen en wijzig de waarde Hallo van **http://localhost:4898/PfWsSdk.asmx** toohello URL van webservice-SDK (voorbeeld: https://mfa.contoso.com/ MultiFactorAuthWebServiceSdk/PfWsSdk.asmx).
   * Sla Hallo Web.Config-bestand op en sluit Kladblok.

   > [!NOTE]
   > Omdat SSL wordt gebruikt voor deze verbinding, moet u verwijzen naar Web Service SDK door Hallo **volledig gekwalificeerde domeinnaam (FQDN)** en **niet IP-adres**. Hallo SSL-certificaat wordt uitgegeven voor Hallo FQDN en hello URL die wordt gebruikt moet overeenkomen met Hallo-naam op Hallo certificaat.

7. Hallo-website die de webservice voor mobiele App is geïnstalleerd met een openbaar ondertekend certificaat niet al is gebonden, Hallo certificaat installeren op Hallo-server, open IIS-beheer als Hallo certificaat toohello website binden.
8. Open een webbrowser op een computer en navigeer toohello-URL waar de webservice voor mobiele App is geïnstalleerd (voorbeeld: https://mfa.contoso.com/MultiFactorAuthMobileAppWebService). Controleer of er geen certificaatwaarschuwingen of -fouten worden weergegeven.

## <a name="configure-hello-mobile-app-settings-in-hello-azure-multi-factor-authentication-server"></a>De instellingen van de mobiele app Hallo in hello Azure multi-factor Authentication-Server configureren

Nu Hallo mobiele app webservice is geïnstalleerd, moet u tooconfigure hello Azure multi-factor Authentication-Server toowork met Hallo-portal.

1. Klik op Hallo Gebruikersportal-pictogram Hallo multi-factor Authentication Server-console. Controleren van hun verificatiemethoden gebruikers zijn niet toegestaan als toocontrol **mobiele App** op Hallo tabblad instellingen onder **toestaan dat gebruikers de methode tooselect**. Zonder deze functie is ingeschakeld, eindgebruikers zijn vereist toocontact uw helpdesk toocomplete activering voor Hallo mobiele App.
2. Controleer de Hallo **toestaan dat gebruikers tooactivate mobiele App** vak.
3. Controleer de Hallo **gebruikersregistratie toestaan** vak.
4. Klik op Hallo **mobiele App** pictogram.
5. Voer Hallo-URL wordt gebruikt met Hallo virtuele map die is gemaakt bij het installeren van MultiFactorAuthenticationMobileAppWebServiceSetup64 (voorbeeld: https://mfa.contoso.com/MultiFactorAuthMobileAppWebService/) in het veld Hallo  **Mobiele Web-App Service-URL:**.
6. Hallo vullen **accountnaam** veld met het bedrijf of organisatie-naam toodisplay Hallo in Hallo mobiele toepassing voor dit account.
   ![Configuratie van MFA-server - instellingen voor mobiele app](./media/multi-factor-authentication-get-started-server-webservice/mobile.png)

## <a name="next-steps"></a>Volgende stappen

- [Geavanceerde scenario's met Azure Multi-Factor Authentication en VPN's van derden](multi-factor-authentication-advanced-vpn-configurations.md).