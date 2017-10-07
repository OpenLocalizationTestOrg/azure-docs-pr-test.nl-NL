---
title: aaaAzure Mobile Engagement Web SDK upgradeprocedures | Microsoft Docs
description: meest recente updates en procedures voor het Hallo Web SDK voor Azure Mobile Engagement Hallo
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a20529b4-ec8d-4503-8ae9-09b5f0846d5b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: a2df65904c6b56584ce6588ed26a9b79f3aa27ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-web-sdk-upgrade-procedures"></a>Azure Mobile Engagement Web SDK upgradeprocedures
Als u hebt al een eerdere versie van Azure Mobile Engagement Web SDK Hallo geïntegreerd in uw webtoepassing, moet u tooconsider Hallo volgende punten wanneer u een upgrade uitvoert van Hallo SDK.

Als u meerdere versies van Mobile Engagement Web SDK Hallo overgeslagen, moet u mogelijk toocomplete verschillende procedures tijdens het upgradeproces Hallo. Bijvoorbeeld, als u migreert vanaf 1.4.0 too1.6.0, eerste Volg Hallo procedures tooupgrade van 1.4.0 too1.5.0. Volg daarna Hallo procedures tooupgrade van 1.5.0 too1.6.0.

Welke versie u een van upgrade, vervangen door een eerdere versie van Hallo bestand azure-engagement.js Hallo meest recente versie van Hallo-bestand.

## <a name="upgrade-from-121-too200"></a>Upgrade van 1.2.1 too2.0.0
Deze sectie beschrijft hoe toomigrate een Mobile Engagement Web SDK-integratie van Hallo Capptain service, die worden aangeboden door Capptain SAS, tooan Azure Mobile Engagement-app. Als u vanaf een eerdere versie, neem Raadpleeg Hallo Capptain website toofirst migreert too1.2.1 migreren en vervolgens toepassen Hallo procedures te volgen.

Deze versie van Hallo Mobile Engagement Web SDK biedt geen ondersteuning voor Samsung Smart TV, Opera TV, webOS of Hallo Reach-functie.

> [!IMPORTANT]
> Capptain en Azure Mobile Engagement zijn niet dezelfde service Hallo. Hallo na procedure licht alleen toomigrate Hallo client-app. Migreren Hallo Mobile Engagement Web SDK in Hallo-app wordt niet uw gegevens migreren vanaf een Capptain tooa Mobile Engagement-server.
> 
> 

### <a name="javascript-files"></a>JavaScript-bestanden
Vervangen Hallo bestand capptain-sdk.js Hello azure engagement.js bestand, en werk uw invoer script vervolgens dienovereenkomstig.

### <a name="remove-capptain-reach"></a>Capptain Reach verwijderen
Deze versie van Hallo Mobile Engagement Web SDK biedt geen ondersteuning voor Hallo Reach-functie. Als u Capptain Reach geïntegreerd in uw toepassing, moet u tooremove deze.

Hallo bereiken CSS importeren uit uw pagina verwijderen en verwijder Hallo gerelateerde CSS-bestand (capptain-reach.css, standaard).

Verwijderen van Hallo Reach-resources te volgen: Hallo Hallo merk-pictogram (standaard capptain-melding-pictogram) en sluiten afbeelding (capptain-close.png, standaard).

Verwijder Hallo UI bereiken voor in-app-meldingen. Hallo-standaardindeling ziet er als volgt:

    <!-- capptain notification -->
    <div id="capptain_notification_area" class="capptain_category_default">
      <div class="icon">
        <img src="capptain-notification-icon.png" alt="icon" />
      </div>
      <div class="content">
        <div class="title" id="capptain_notification_title"></div>
        <div class="message" id="capptain_notification_message"></div>
      </div>
      <div id="capptain_notification_image"></div>
      <div>
        <button id="capptain_notification_close">Close</button>
      </div>
    </div>

Hallo UI bereiken voor tekst- en aankondigingen en polls verwijderen. Hallo-standaardindeling ziet er als volgt:

    <div id="capptain_overlay" class="capptain_category_default">
      <button id="capptain_overlay_close">x</button>
      <div id="capptain_overlay_title"></div>
      <div id="capptain_overlay_body"></div>
      <div id="capptain_overlay_poll"></div>
      <div id="capptain_overlay_buttons">
        <button id="capptain_overlay_exit"></button>
        <button id="capptain_overlay_action"></button>
      </div>
    </div>

Hallo verwijderen `reach` object uit uw configuratie, indien aanwezig. Als volgt uitziet:

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

Verwijder eventuele andere Reach-aanpassing, zoals categorieën.

### <a name="remove-deprecated-apis"></a>Afgeschafte API's verwijderen
Sommige-API's van Capptain zijn afgeschaft in Hallo Mobile Engagement Web SDK.

Verwijder alle aanroepen toohello API's te volgen: `agent.connect`, `agent.disconnect`, `agent.pause`, en `agent.sendMessageToDevice`.

Verwijder alle exemplaren van de volgende retouraanroepen uit de configuratie van uw Capptain Hallo: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, en `onPushMessageReceived`.

### <a name="configuration"></a>Configuratie
Mobile Engagement maakt gebruik van een verbinding tekenreeks tooconfigure SDK-id's, bijvoorbeeld Hallo toepassings-id.

Hallo toepassings-ID vervangen door de verbindingsreeks. Houd er rekening mee dat globale Hallo-object voor Hallo SDK-configuratie wordt gewijzigd van `capptain` te`azureEngagement`.

Vóór de migratie:

    window.capptain = {
      appId: ...,
      [...]
    };

Na de migratie:

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

Hallo-verbindingsreeks voor uw toepassing wordt weergegeven in hello Azure-Portal.

### <a name="javascript-apis"></a>JavaScript-API 's
Hallo globale JavaScript-object `window.capptain` heeft gekregen `window.azureEngagement` , maar u kunt Hallo `window.engagement` alias voor de API-aanroepen. U kunt Hallo alias toodefine Hallo SDK configuratie niet gebruiken.

Bijvoorbeeld: `capptain.deviceId` wordt `engagement.deviceId`, `capptain.agent.startActivity` wordt `engagement.agent.startActivity`, enzovoort.

