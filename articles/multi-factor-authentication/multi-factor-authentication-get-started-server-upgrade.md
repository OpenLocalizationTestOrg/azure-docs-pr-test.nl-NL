---
title: aaaUpgrade PhoneFactor tooAzure MFA-Server | Microsoft Docs
description: Aan de slag met Azure MFA-Server wanneer u een upgrade van Hallo oudere phonefactor-agent uitvoert.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 42838ff7-bdf2-4d06-bacc-b3839a00cd76
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.openlocfilehash: 15b7b8517929c30f66e6a39cd44c69d12d25c6d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-hello-phonefactor-agent-tooazure-multi-factor-authentication-server"></a>Hallo PhoneFactor Agent tooAzure multi-factor Authentication-Server bijwerken
tooupgrade hello PhoneFactor Agent versie 5.x of oudere tooAzure multi-factor Authentication-Server, Hallo PhoneFactor Agent verwijderen en eerst onderdelen gekoppeld. Vervolgens Hallo multi-factor Authentication-Server en de verbonden onderdelen kunnen worden geïnstalleerd.

## <a name="uninstall-hello-phonefactor-agent"></a>Hallo PhoneFactor Agent verwijderen

1. Ten eerste back-up Hallo PhoneFactor-gegevensbestand. Hallo standaardlocatie voor installatie is C:\Program Files\PhoneFactor\Data\Phonefactor.pfdata.

2. Hallo Gebruikersportal is geïnstalleerd:
  1. Navigeer installatiemap toohello en back-up Hallo web.config-bestand. Hallo standaardlocatie voor installatie is C:\inetpub\wwwroot\PhoneFactor.

  2. Als u aangepaste thema's toohello portal hebt toegevoegd, back-up van uw aangepaste map onder Hallo C:\inetpub\wwwroot\PhoneFactor\App_Themes directory.

  3. Hallo Gebruikersportal via Hallo PhoneFactor Agent verwijderen (alleen beschikbaar als geïnstalleerd op Hallo dezelfde server als Hallo PhoneFactor Agent) of via Windows-programma's en onderdelen.

3. Hallo webservice voor mobiele App is geïnstalleerd:

  1. Ga toohello installatiemap en back-up Hallo web.config-bestand. Hallo standaardlocatie voor installatie is C:\inetpub\wwwroot\PhoneFactorPhoneAppWebService.

  2. Hallo Mobile App Web Service via Windows-programma's en onderdelen verwijderen.

4. Als Hallo Web Service SDK is geïnstalleerd, moet u het verwijdert via Hallo PhoneFactor Agent of via Windows programma's en onderdelen.

5. Hallo PhoneFactor Agent via Windows programma's en onderdelen verwijderen.

## <a name="install-hello-multi-factor-authentication-server"></a>Hallo multi-factor Authentication-Server installeren

Hallo installatiepad wordt opgehaald uit het register van de vorige PhoneFactor Agent installatie Hallo Hallo is dus in Hallo dezelfde locatie (bijvoorbeeld C:\Program Files\PhoneFactor). Nieuwe installaties hebben een ander standaardinstallatiepad (bijvoorbeeld C:\Program Files\Multi-Factor Authentication Server). Hallo gegevensbestand van Hallo vorige die phonefactor Agent moet worden bijgewerkt tijdens de installatie van uw gebruikers en -instellingen moeten dus nog steeds Hallo er na het installeren van nieuwe multi-factor Authentication-Server.

1. Als u wordt gevraagd, Hallo multi-factor Authentication-Server activeren en zorg ervoor dat de juiste replicatiegroep toohello is toegewezen.

2. Hallo nieuwe webservice-SDK via de gebruikersinterface van multi-factor Authentication Server Hallo als Hallo Web Service SDK eerder was geïnstalleerd, installeert.

  de naam van de virtuele map nu is standaard Hallo **MultiFactorAuthWebServiceSdk** in plaats van **PhoneFactorWebServiceSdk**. Als u toouse Hallo oude naam wilt, moet u Hallo-naam van de virtuele map Hallo tijdens de installatie wijzigen. Anders, als u Hallo installeren toouse Hallo nieuwe standaardnaam toestaat, hebt u toochange Hallo URL in alle toepassingen die verwijzing Hallo toopoint Web Service SDK (zoals Hallo Gebruikersportal en de webservice voor mobiele App) op de juiste locatie Hallo.

3. Hallo nieuwe multi-factor Authentication-Gebruikersportal via de gebruikersinterface van multi-factor Authentication Server Hallo als Hallo Gebruikersportal eerder was geïnstalleerd op Hallo PhoneFactor Agent-Server installeert.

  de naam van de virtuele map nu is standaard Hallo **MultiFactorAuth** in plaats van **PhoneFactor**. Als u toouse Hallo oude naam wilt, moet u Hallo-naam van de virtuele map Hallo tijdens de installatie wijzigen. Als u Hallo installeren toouse Hallo nieuwe standaardnaam toestaat, moet u klikt u op Hallo Gebruikersportal-pictogram in Hallo multi-factor Authentication-Server en Hallo Gebruikersportal-URL op tabblad Hallo-instellingen bijwerken.

4. Hallo PhoneFactor Agent als Hallo Gebruikersportal en/of webservice voor mobiele Apps eerder was geïnstalleerd op een andere server uit:

  1. Ga toohello installatielocatie (bijvoorbeeld C:\Program Files\PhoneFactor) en kopieer de installatieprogramma's toohello voor een of meer andere server. Er zijn 32-bits en 64-bits installatieprogramma's voor zowel de Hallo Gebruikersportal als de webservice voor mobiele App. Deze heten MultiFactorAuthenticationUserPortalSetupXX.msi en MultiFactorAuthenticationMobileAppWebServiceSetupXX.msi.

  2. tooinstall hello Gebruikersportal op de webserver hello, open een opdrachtprompt als beheerder en voer MultiFactorAuthenticationUserPortalSetupXX.msi uit.

    de naam van de virtuele map nu is standaard Hallo **MultiFactorAuth** in plaats van **PhoneFactor**. Als u toouse Hallo oude naam wilt, moet u Hallo-naam van de virtuele map Hallo tijdens de installatie wijzigen. Als u Hallo installeren toouse Hallo nieuwe standaardnaam toestaat, moet u klikt u op Hallo Gebruikersportal-pictogram in Hallo multi-factor Authentication-Server en Hallo Gebruikersportal-URL op tabblad Hallo-instellingen bijwerken. Bestaande gebruikers moeten op de hoogte van de nieuwe URL Hallo toobe.

  3. Ga toohello Gebruikersportal installatielocatie (bijvoorbeeld C:\inetpub\wwwroot\MultiFactorAuth) en Hallo web.config-bestand bewerken. Hallo-waarden in Hallo secties appSettings en applicationSettings van het oorspronkelijke web.config-bestand dat een back-up vóór de upgrade Hallo naar het nieuwe bestand web.config Hallo kopiëren. Als Hallo nieuwe virtuele map standaardnaam bij de installatie van Web Service SDK Hallo aangehouden is, wijzigt u Hallo-URL op Hallo applicationSettings sectie toopoint toohello juiste locatie. Als er nog andere standaardinstellingen zijn gewijzigd in het vorige bestand web.config hello, van toepassing die dezelfde wijzigingen toohello nieuwe bestand web.config.

  4. tooinstall hello webservice voor mobiele App op de webserver hello, open een opdrachtprompt als beheerder en Voer Hallo MultiFactorAuthenticationMobileAppWebServiceSetupXX.msi uit.

    de naam van de virtuele map nu is standaard Hallo **MultiFactorAuthMobileAppWebService** in plaats van **PhoneFactorPhoneAppWebService**. Als u toouse Hallo oude naam wilt, moet u Hallo-naam van de virtuele map Hallo tijdens de installatie wijzigen. U kunt een kortere naam toomake toochoose gemakkelijk voor eindgebruikers tootype in op hun mobiele apparaten. Klik anders als u Hallo installeren toouse Hallo nieuwe standaardnaam toestaat, moet u op pictogram van de mobiele App Hallo op Hallo multi-factor Authentication-Server en Hallo Mobile App Web Service-URL bijwerken.

  5. Ga locatie toohello webservice voor mobiele App is geïnstalleerd (bijvoorbeeld C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService) en Hallo web.config-bestand bewerken. Hallo-waarden in Hallo secties appSettings en applicationSettings van het oorspronkelijke web.config-bestand dat een back-up vóór de upgrade Hallo naar het nieuwe bestand web.config Hallo kopiëren. Als Hallo nieuwe virtuele map standaardnaam bij de installatie van Web Service SDK Hallo aangehouden is, wijzigt u Hallo-URL op Hallo applicationSettings sectie toopoint toohello juiste locatie. Als er nog andere standaardinstellingen zijn gewijzigd in het vorige bestand web.config hello, van toepassing die dezelfde wijzigingen toohello nieuwe bestand web.config.

## <a name="next-steps"></a>Volgende stappen

- [Hallo-portal voor gebruikers installeren](multi-factor-authentication-get-started-portal.md) voor hello Azure multi-factor Authentication-Server.

- [Windows-verificatie configureren](multi-factor-authentication-get-started-server-windows.md) voor uw toepassingen. 
