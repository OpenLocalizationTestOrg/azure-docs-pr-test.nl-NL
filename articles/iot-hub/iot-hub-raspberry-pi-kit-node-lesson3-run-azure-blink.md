---
title: 'Verbinding maken met frambozen Pi (knooppunt) tooAzure IoT - les 3: voorbeeld uitvoeren | Microsoft Docs'
description: Implementeren en uitvoeren van een steekproef toepassing tooRaspberry Pi 3 dat berichten tooyour iothub verzendt en Hallo LED knippert.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: knipperen cloud pi geleid, knipperen geleid vanuit de cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 427d8e5e-8af8-4249-8607-44edc90a4972
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 991c64e0b1b6f965b029560cdc6403e557841e30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>Uitvoeren van een toepassing voorbeeld toosend apparaat-naar-cloud-berichten
## <a name="what-you-will-do"></a>Wat u doet
Dit artikel wordt beschreven hoe toodeploy en een voorbeeld van een toepassing wordt uitgevoerd op frambozen Pi 3 dat verzendt berichten tooyour IoT-hub. Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Wat u leert
U leert hoe toouse hello gulp hulpprogramma toodeploy en Hallo voorbeeld Node.js-toepassing uitvoeren op Pi.

## <a name="what-you-need"></a>Wat u nodig hebt
* Voordat u deze taak moet is voltooid [maken van een Azure-functie-app en een storage account tooprocess en store iothub berichten](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md).

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Ophalen van uw IoT-hub en apparaat-verbindingsreeksen
Hallo apparaat verbindingsreeks wordt gebruikt door uw Pi tooconnect tooyour IoT-hub. Hallo IoT hub-verbindingsreeks is gebruikte tooconnect toohello-identiteitenregister van uw IoT hub toomanage Hallo-apparaten die zijn toegestaan tooconnect tooyour IoT-hub. 

* Een overzicht van uw IoT-hubs in uw resourcegroep door het uitvoeren van hello Azure CLI-opdracht te volgen:

```bash
az iot hub list -g iot-sample --query [].name
```

Gebruik `iot-sample` als Hallo-waarde van `{resource group name}` als u Hallo-waarde niet wijzigt.

* Hallo IoT hub-verbindingsreeks ophalen door het uitvoeren van hello Azure CLI-opdracht te volgen:

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

`{my hub name}`Hallo-naam die u hebt opgegeven als u uw IoT-hub gemaakt en geregistreerd Pi is.

* Hallo apparaat-verbindingsreeks ophalen door het uitvoeren van de volgende opdracht Hallo:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

Gebruik `myraspberrypi` als Hallo-waarde van `{device id}` als u Hallo-waarde niet wijzigt.

## <a name="configure-hello-device-connection"></a>Hallo apparaatverbinding configureren
1. Hallo-configuratiebestand door het uitvoeren van de volgende opdrachten Hallo initialiseren:
   
   ```bash
   npm install
   gulp init
   ```
2. Open Hallo apparaat configuratiebestand `config-raspberrypi.json` in Visual Studio Code door te voeren Hallo volgende opdracht:
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
  
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
  
   ![Config.JSON](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. Zorg Hallo vervangingen in Hallo na `config-raspberrypi.json` bestand:
   
   * Vervang **[apparaat-hostnaam of IP-adres]** met Hallo IP-adres of de hostnaam apparaatnaam u gekregen `device-discovery-cli` of Hallo waarde overgenomen wanneer u uw apparaat geconfigureerd.
   * Vervang **[apparaat-verbindingsreeks IoT]** Hello `device connection string` u hebt verkregen.
   * Vervang **[IoT hub verbindingsreeks]** Hello `iot hub connection string` u hebt verkregen.

Update Hallo `config-raspberrypi.json` bestand zodat u de voorbeeldtoepassing Hallo van uw computer kunt implementeren.

## <a name="deploy-and-run-hello-sample-application"></a>Implementeren en uitvoeren van de voorbeeldtoepassing Hallo
Implementeren en uitvoeren van de voorbeeldtoepassing Hallo op Pi door het uitvoeren van de volgende opdracht Hallo:

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a>Controleer of de voorbeeldtoepassing Hallo werkt
U ziet Hallo LED die is verbonden tooPi knippert elke twee seconden. Telkens wanneer Hallo LED knippert, wordt de voorbeeldtoepassing Hallo verzendt een bericht tooyour IoT-hub en verifieert dat het Hallo-bericht is verzonden tooyour IoT-hub. Bovendien wordt elk bericht ontvangen door de IoT-hub Hallo afgedrukt in het consolevenster Hallo. Hallo-voorbeeldtoepassing wordt automatisch beëindigd na 20 berichten verzenden.

![Voorbeeld van een toepassing met verzonden en ontvangen van berichten](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run.png)

## <a name="summary"></a>Samenvatting
U hebt geïmplementeerd en nieuwe knipperen Hallo-voorbeeldtoepassing uitvoeren op Pi toosend apparaat-naar-cloudberichten tooyour iothub. U kunt nu uw berichten bewaken als ze toohello opslagaccount zijn geschreven.

## <a name="next-steps"></a>Volgende stappen
[Alleen berichten permanent in Azure Storage](iot-hub-raspberry-pi-kit-node-lesson3-read-table-storage.md)

