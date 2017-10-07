---
title: 'Verbinding maken met Intel Edison (knooppunt) tooAzure IoT - les 3: berichten verzenden | Microsoft Docs'
description: Implementeren en uitvoeren van een steekproef toepassing tooIntel Edison dat berichten tooyour iothub verzendt en Hallo LED knippert.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: IOT-cloudservice, arduino verzenden gegevens toocloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 1b3b1074-f4d4-42ac-b32c-55f18b304b44
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ebd4c7558544d64086fb4cd615cee546aeed2fc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>Uitvoeren van een toepassing voorbeeld toosend apparaat-naar-cloud-berichten
## <a name="what-you-will-do"></a>Wat u doet
Dit artikel wordt beschreven hoe toodeploy en een voorbeeld van een toepassing wordt uitgevoerd op Intel Edison die verzendt berichten tooyour IoT-hub. Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].

## <a name="what-you-will-learn"></a>Wat u leert
U leert hoe toouse Hallo hulpprogramma toodeploy gulp en Hallo C voorbeeldtoepassing uitvoeren op Edison.

## <a name="what-you-need"></a>Wat u nodig hebt
* Voordat u deze taak moet is voltooid [maken van een Azure-functie-app en een storage account tooprocess en store iothub berichten][process-and-store-iot-hub-messages].

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Ophalen van uw IoT-hub en apparaat-verbindingsreeksen
Hallo apparaat-verbindingsreeks is gebruikte tooconnect Edison tooyour IoT-hub. Hallo IoT hub-verbindingsreeks is gebruikte tooconnect uw IoT hub toohello apparaat-id die Edison in Hallo IoT-hub aangeeft.

* Een overzicht van uw IoT-hubs in uw resourcegroep door het uitvoeren van hello Azure CLI-opdracht te volgen:

```bash
az iot hub list -g iot-sample --query [].name
```

Gebruik `iot-sample` als Hallo-waarde van `{resource group name}` als u Hallo-waarde niet wijzigt.

* Hallo IoT hub-verbindingsreeks ophalen door het uitvoeren van hello Azure CLI-opdracht te volgen:

```bash
az iot hub show-connection-string --name {my hub name}
```

`{my hub name}`Hallo-naam die u hebt opgegeven als u uw IoT-hub gemaakt en geregistreerd Edison is.

* Hallo apparaat-verbindingsreeks ophalen door het uitvoeren van de volgende opdracht Hallo:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

Gebruik `myinteledison` als Hallo-waarde van `{device id}` als u Hallo-waarde niet wijzigt.

## <a name="configure-hello-device-connection"></a>Hallo apparaatverbinding configureren
1. Hallo-configuratiebestand door het uitvoeren van de volgende opdrachten Hallo initialiseren:

   ```bash
   npm install
   gulp init
   ```

2. Open Hallo apparaat configuratiebestand `config-edison.json` in Visual Studio Code door te voeren Hallo volgende opdracht:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![Config.JSON](media/iot-hub-intel-edison-lessons/lesson3/config.png)
3. Zorg Hallo vervangingen in Hallo na `config-edison.json` bestand:

   * Vervang **[apparaat-hostnaam of IP-adres]** met Hallo apparaat IP-adres u omlaag gemarkeerd wanneer u uw apparaat geconfigureerd.
   * Vervang **[apparaat-verbindingsreeks IoT]** Hello `device connection string` u hebt verkregen.
   * Vervang **[IoT hub verbindingsreeks]** Hello `iot hub connection string` u hebt verkregen.

   > [!NOTE]
   > U hoeft niet `azure_storage_connection_string` in dit artikel. Houd deze zo is.

## <a name="deploy-and-run-hello-sample-application"></a>Implementeren en uitvoeren van de voorbeeldtoepassing Hallo
Implementeren en uitvoeren van de voorbeeldtoepassing Hallo op Edison door het uitvoeren van de volgende opdracht Hallo:

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a>Controleer of de voorbeeldtoepassing Hallo werkt
U ziet Hallo LED die is verbonden tooEdison knippert elke twee seconden. Telkens wanneer Hallo LED knippert, wordt de voorbeeldtoepassing Hallo verzendt een bericht tooyour IoT-hub en verifieert dat het Hallo-bericht is verzonden tooyour IoT-hub. Bovendien wordt elk bericht ontvangen door de IoT-hub Hallo afgedrukt in het consolevenster Hallo. Hallo-voorbeeldtoepassing wordt automatisch beëindigd na 20 berichten verzenden.

![Voorbeeld van een toepassing met verzonden en ontvangen van berichten][sample-application-with-sent-and-received-messages]

## <a name="summary"></a>Samenvatting
U hebt geïmplementeerd en nieuwe knipperen Hallo-voorbeeldtoepassing uitvoeren op Edison toosend apparaat-naar-cloudberichten tooyour IoT-hub. U nu bewaken uw berichten zoals ze zijn toohello storage-account geschreven.

## <a name="next-steps"></a>Volgende stappen
[Alleen berichten permanent in Azure Storage][read-messages-persisted-in-azure-storage]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-node-lesson3-read-table-storage.md