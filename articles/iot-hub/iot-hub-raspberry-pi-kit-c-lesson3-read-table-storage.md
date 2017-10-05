---
title: 'Connect Raspberry PI (C) naar Azure IoT - les 3: Table storage | Microsoft Docs'
description: De apparaat-naar-cloud-berichten bewaken omdat ze naar uw Azure Table-opslag zijn geschreven.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: gegevens ophalen uit de cloud, iot-cloudservice
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 8c5558bb-3c31-4445-90e6-b1a978738545
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 16b7f2e38bfe3b40d199cb6e07976433aa54ea32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a>Alleen berichten permanent in Azure Storage
## <a name="what-you-will-do"></a>Wat u doet
Controleer de apparaat-naar-cloud-berichten die vanaf frambozen Pi 3 naar uw IoT-hub worden verzonden omdat de berichten naar uw Azure Table-opslag zijn geschreven. Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u hoe u met de taak bericht lezen gulp lezen berichten permanent in uw Azure Table-opslag.

## <a name="what-you-need"></a>Wat u nodig hebt
Voordat u deze procedure begint, moet is voltooid [uitvoeren van de voorbeeldtoepassing Azure knipperen op frambozen Pi 3](iot-hub-raspberry-pi-kit-c-lesson3-run-azure-blink.md).

## <a name="read-new-messages-from-your-storage-account"></a>Nieuwe berichten in uw storage-account lezen
In het vorige artikel kunt u een voorbeeld van toepassing op Pi uitgevoerd. De voorbeeld-toepassing verzonden berichten naar uw Azure-IoT-hub. De verzonden naar uw IoT-hub berichten worden opgeslagen in uw Azure Table storage via de Azure-functie-app. U moet de verbindingsreeks voor Azure-opslag om berichten te lezen uit uw Azure-tabelopslag.

Als u wilt lezen van berichten die zijn opgeslagen in uw Azure Table storage, de volgende stappen uit:

1. De verbindingsreeks ophalen met de volgende opdrachten:

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   De eerste opdracht haalt de `storage name` die wordt gebruikt in de tweede opdracht om de verbindingsreeks ophalen. Gebruik `iot-sample` als de waarde van `{resource group name}` als u de waarde niet wijzigen.
2. Open het configuratiebestand `config-raspberrypi.json` in Visual Studio Code met de volgende opdracht:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
3. Vervang `[Azure storage connection string]` met de verbindingsreeks die u in stap 1 hebt verkregen.
4. Sla de `config-raspberrypi.json` bestand.
5. Berichten opnieuw verzenden en ze uit uw Azure-tabelopslag lezen door de volgende opdracht uit te voeren:
   
   ```bash
   gulp run --read-storage
   ```
   
   De logica voor het lezen van Azure Table storage is in de `azure-table.js` bestand.
   
   ![gulp uitgevoerd--lezen-opslag](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_read_message_c.png)

## <a name="summary"></a>Samenvatting
U hebt met succes Pi verbonden met uw IoT-hub in de cloud en de voorbeeldtoepassing knipperen gebruikt om apparaat-naar-cloud-berichten te verzenden. U hebt ook de functie Azure-app gebruikt voor het opslaan van IoT hub berichten naar uw Azure Table-opslag. Nu kunt u cloud-naar-apparaat-berichten verzenden van uw IoT-hub tot Pi.

## <a name="next-steps"></a>Volgende stappen
[Voer een voorbeeldtoepassing cloud-naar-apparaat-berichten ontvangen](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md)

