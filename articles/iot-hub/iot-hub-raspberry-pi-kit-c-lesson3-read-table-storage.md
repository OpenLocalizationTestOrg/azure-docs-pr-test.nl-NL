---
title: 'Connect Raspberry PI (C) tooAzure IoT - les 3: Table storage | Microsoft Docs'
description: Hallo apparaat-naar-cloud-berichten bewaken tijdens deze tooyour Azure Table storage worden geschreven.
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
ms.openlocfilehash: 307ce2bc595339790db7379cc011fe262c2b8734
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a>Alleen berichten permanent in Azure Storage
## <a name="what-you-will-do"></a>Wat u doet
Monitor Hallo apparaat-naar-cloud-berichten dat uit frambozen Pi 3 tooyour iothub worden verzonden als Hallo-berichten worden geschreven tooyour Azure Table storage. Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u hoe toouse hello gulp bericht lezen taak tooread-berichten permanent in uw Azure Table-opslag.

## <a name="what-you-need"></a>Wat u nodig hebt
Voordat u deze procedure begint, moet is voltooid [hello Azure knipperen voorbeeldtoepassing uitvoeren op frambozen Pi 3](iot-hub-raspberry-pi-kit-c-lesson3-run-azure-blink.md).

## <a name="read-new-messages-from-your-storage-account"></a>Nieuwe berichten in uw storage-account lezen
In het vorige artikel hello, kunt u een voorbeeld van toepassing op Pi uitgevoerd. Hallo-voorbeeldtoepassing verzonden berichten tooyour Azure IoT hub. IoT-hub tooyour verzonden Hello-berichten worden opgeslagen in uw Azure-tabelopslag via hello Azure functie-app. U moet Hallo Azure storage connection string tooread berichten uit uw Azure-tabelopslag.

tooread berichten die zijn opgeslagen in uw Azure Table storage, als volgt te werk:

1. Hallo-verbindingsreeks ophalen door het uitvoeren van de volgende opdrachten Hallo:

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   de eerste opdracht Hallo haalt Hallo `storage name` die wordt gebruikt in Hallo tweede opdracht tooget Hallo verbindingsreeks. Gebruik `iot-sample` als Hallo-waarde van `{resource group name}` als u Hallo-waarde niet wijzigt.
2. Open Hallo-configuratiebestand `config-raspberrypi.json` in Visual Studio Code door te voeren Hallo volgende opdracht:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
3. Vervang `[Azure storage connection string]` met Hallo-verbindingsreeks die u in stap 1 hebt verkregen.
4. Hallo opslaan `config-raspberrypi.json` bestand.
5. Berichten opnieuw verzenden en ze door het uitvoeren van de volgende opdracht Hallo uit uw Azure-tabelopslag lezen:
   
   ```bash
   gulp run --read-storage
   ```
   
   Hallo logica voor het lezen van Azure Table storage is in Hallo `azure-table.js` bestand.
   
   ![gulp uitgevoerd--lezen-opslag](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_read_message_c.png)

## <a name="summary"></a>Samenvatting
U hebt met succes Pi tooyour iothub in de cloud Hallo verbonden en hello knipperen voorbeeld toepassing toosend apparaat-naar-cloud-berichten gebruikt. U hebt ook hello Azure functie app toostore binnenkomende IoT hub berichten tooyour Azure Table-opslag gebruikt. Nu kunt u cloud-naar-apparaat-berichten verzenden van uw IoT hub tooPi.

## <a name="next-steps"></a>Volgende stappen
[Uitvoeren van een toepassing voorbeeld tooreceive cloud-naar-apparaat-berichten](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md)

