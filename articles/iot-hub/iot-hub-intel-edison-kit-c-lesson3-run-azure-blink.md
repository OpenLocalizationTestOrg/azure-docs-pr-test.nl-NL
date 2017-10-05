---
title: 'Connect Intel Edison (C) naar Azure IoT - les 3: berichten verzenden | Microsoft Docs'
description: Implementeren en uitvoeren van een voorbeeld van toepassing op Intel Edison dat berichten verzendt naar uw IoT-hub en de LED knippert.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: IOT-cloudservice, arduino verzenden van gegevens naar de cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 12672b64-795a-4dfc-86fd-df53ed3eeef7
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d104618ebb37a19c83f161beceb5c71bc89bbb56
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a>Voer een voorbeeldtoepassing om apparaat-naar-cloud-berichten te verzenden
## <a name="what-you-will-do"></a>Wat u doet
In dit artikel wordt beschreven hoe u implementeren en uitvoeren van een voorbeeld van toepassing op Intel Edison dat berichten naar uw IoT-hub verzendt. Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina][troubleshooting].

## <a name="what-you-will-learn"></a>Wat u leert
U leert hoe u met het hulpprogramma gulp implementeren en uitvoeren van de voorbeeldtoepassing C op Edison.

## <a name="what-you-need"></a>Wat u nodig hebt
* Voordat u deze taak moet is voltooid [maken van een Azure-functie-app en een opslagaccount om te verwerken en opslaan van IoT hub berichten][process-and-store-iot-hub-messages].

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Ophalen van uw IoT-hub en apparaat-verbindingsreeksen
De verbindingsreeks van het apparaat wordt gebruikt voor Edison verbinding met uw IoT-hub. De verbindingsreeks van de IoT-hub wordt gebruikt voor het verbinden van uw IoT-hub met de apparaat-id die Edison in de IoT-hub vertegenwoordigt.

* Een overzicht van uw IoT-hubs in de resourcegroep met de volgende Azure CLI-opdracht:

```bash
az iot hub list -g iot-sample --query [].name
```

Gebruik `iot-sample` als de waarde van `{resource group name}` als u de waarde niet wijzigen.

* De IoT hub-verbindingsreeks ophalen met de volgende opdracht in de Azure CLI:

```bash
az iot hub show-connection-string --name {my hub name}
```

`{my hub name}`is de naam die u hebt opgegeven als u uw IoT-hub gemaakt en geregistreerd Edison.

* De apparaat-verbindingsreeks ophalen met de volgende opdracht:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

Gebruik `myinteledison` als de waarde van `{device id}` als u de waarde niet wijzigen.

## <a name="configure-the-device-connection"></a>De apparaatverbinding configureren
1. Het configuratiebestand initialiseren met de volgende opdrachten:

   ```bash
   npm install
   gulp init
   ```
   > [!NOTE]
   > Voer **gulp install-hulpprogramma's** en, als u dit nog niet hebt gedaan in les 1.

2. Open het configuratiebestand van het apparaat `config-edison.json` in Visual Studio Code met de volgende opdracht:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![Config.JSON](media/iot-hub-intel-edison-lessons/lesson3/config.png)

3. Controleer de volgende vervangingen in de `config-edison.json` bestand:

   * Vervang **[apparaat-hostnaam of IP-adres]** met het apparaat IP-adres dat u naar beneden gemarkeerd wanneer u uw apparaat geconfigureerd.
   * Vervang **[apparaat-verbindingsreeks IoT]** met de `device connection string` u hebt verkregen.
   * Vervang **[IoT hub verbindingsreeks]** met de `iot hub connection string` u hebt verkregen.

   > [!NOTE]
   > U hoeft niet `azure_storage_connection_string` in dit artikel. Houd deze zo is.

## <a name="deploy-and-run-the-sample-application"></a>Implementeren en uitvoeren van de voorbeeldtoepassing
Implementeren en uitvoeren van de voorbeeldtoepassing op Edison met de volgende opdracht:

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a>Controleer of de voorbeeldtoepassing werkt
U ziet de LED die is verbonden met Edison knippert elke twee seconden. Telkens wanneer de LED knippert, wordt de voorbeeldtoepassing verzendt een bericht naar uw IoT-hub en verifieert dat wordt het bericht is verzonden naar uw IoT-hub. Bovendien wordt elk bericht ontvangen door de IoT-hub in het consolevenster. De voorbeeldtoepassing wordt automatisch beëindigd na 20 berichten verzenden.

![Voorbeeld van een toepassing met verzonden en ontvangen van berichten][sample-application-with-sent-and-received-messages]

## <a name="summary"></a>Samenvatting
U hebt geïmplementeerd en de nieuwe knipperen voorbeeldtoepassing uitvoeren op Edison apparaat-naar-cloud-berichten verzenden naar uw IoT-hub. U nu bewaken uw berichten zoals ze zijn geschreven naar het opslagaccount.

## <a name="next-steps"></a>Volgende stappen
[Alleen berichten permanent in Azure Storage][read-messages-persisted-in-azure-storage]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run_c.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-c-lesson3-read-table-storage.md