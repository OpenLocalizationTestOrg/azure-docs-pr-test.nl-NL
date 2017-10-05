---
title: 'Intel Edison (knooppunt) verbinden met Azure IoT - les 3: berichten | Microsoft Docs'
description: De apparaat-naar-cloud-berichten bewaken omdat ze naar uw Azure Table-opslag zijn geschreven.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: gegevens in de cloud, cloud gegevensverzameling, iot-cloudservice, iot-gegevens
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: fa2c7efe-7e34-4e39-bb70-015c15ac69ed
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c1a59227cd2bf9d2c9bcaa4212dd5127a95e2779
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a>Alleen berichten permanent in Azure Storage
## <a name="what-you-will-do"></a>Wat u doet
Controleer de apparaat-naar-cloud-berichten die vanaf Intel Edison naar uw IoT-hub worden verzonden omdat de berichten naar uw Azure Table-opslag zijn geschreven. Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina][troubleshooting].

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u hoe u met de taak bericht lezen gulp lezen berichten permanent in uw Azure Table-opslag.

## <a name="what-you-need"></a>Wat u nodig hebt
Voordat u deze procedure begint, moet is voltooid [uitvoeren van de voorbeeldtoepassing Azure knipperen op Intel Edison][run-the-azure-blink-sample-application-on-intel-edison].

## <a name="read-new-messages-from-your-storage-account"></a>Nieuwe berichten in uw storage-account lezen
In het vorige artikel kunt u een voorbeeld van toepassing op Edison uitgevoerd. De voorbeeld-toepassing verzonden berichten naar uw Azure-IoT-hub. De verzonden naar uw IoT-hub berichten worden opgeslagen in uw Azure Table storage via de Azure-functie-app. U moet de verbindingsreeks voor Azure-opslag om berichten te lezen uit uw Azure-tabelopslag.

Als u wilt lezen van berichten die zijn opgeslagen in uw Azure Table storage, de volgende stappen uit:

1. De verbindingsreeks ophalen met de volgende opdrachten:

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   De eerste opdracht haalt de `storage name` die wordt gebruikt in de tweede opdracht om de verbindingsreeks ophalen. Gebruik `iot-sample` als de waarde van `{resource group name}` als u de waarde niet wijzigen.
2. Open het configuratiebestand `config-edison.json` in Visual Studio Code met de volgende opdracht:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```
3. Vervang `[Azure storage connection string]` met de verbindingsreeks die u in stap 1 hebt verkregen.
4. Sla de `config-edison.json` bestand.
5. Berichten opnieuw verzenden en ze uit uw Azure-tabelopslag lezen door de volgende opdracht uit te voeren:

   ```bash
   gulp run --read-storage
   ```

   De logica voor het lezen van Azure Table storage is in de `azure-table.js` bestand.

   ![gulp uitgevoerd--lezen-opslag][gulp run]

## <a name="summary"></a>Samenvatting
U hebt met succes Edison verbonden met uw IoT-hub in de cloud en de voorbeeldtoepassing knipperen gebruikt om apparaat-naar-cloud-berichten te verzenden. U hebt ook de functie Azure-app gebruikt voor het opslaan van IoT hub berichten naar uw Azure Table-opslag. U kunt nu naar Edison cloud-naar-apparaat-berichten verzenden van uw IoT-hub.

## <a name="next-steps"></a>Volgende stappen
[Voer een voorbeeldtoepassing cloud-naar-apparaat-berichten ontvangen][receive-cloud-to-device-messages]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[run-the-azure-blink-sample-application-on-intel-edison]: iot-hub-intel-edison-kit-node-lesson3-run-azure-blink.md
[gulp run]: media/iot-hub-intel-edison-lessons/lesson3/gulp_read_message.png
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-node-lesson4-send-cloud-to-device-messages.md