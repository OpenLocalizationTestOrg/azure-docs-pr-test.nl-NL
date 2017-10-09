---
title: 'Gesimuleerde apparaat & Azure IoT Gateway - les 4: Table storage | Microsoft Docs'
description: Berichten uit iothub van Intel NUC tooyour opslaan, tooAzure Table storage geschreven en ze vervolgens vanuit de cloud hello te lezen.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: gegevens ophalen uit de cloud, iot-cloudservice
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 78e4b6ea-968d-401e-a7dc-8f9acdb3ec1a
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 43e299d63bbbe10d4d867af25e700c3a7cc07c53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a>Alleen berichten permanent in Azure Table storage

## <a name="what-you-will-do"></a>Wat u doet

- Hallo gateway voorbeeldtoepassing uitvoeren op uw gateway waarmee berichten tooyour iothub worden verzonden.
- Voorbeeldcode uitvoeren op uw host computer tooread berichten in uw Azure Table-opslag.

Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Wat u leert

Hoe gulp toouse Hallo hulpprogramma toorun Hallo voorbeeld code tooread berichten in uw Azure Table-opslag.

## <a name="what-you-need"></a>Wat u nodig hebt

U hebt met succes Hallo volgende taken:

- [Hello Azure functie-app en hello Azure storage-account gemaakt](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md).
- [Hallo gateway voorbeeldtoepassing uitvoeren](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).
- [Lezen van berichten uit uw IoT-hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md).

## <a name="get-your-azure-storage-connection-strings"></a>Uw Azure storage-verbindingsreeksen ophalen

In deze les vroeg u een Azure storage-account gemaakt. Hallo verbindingsreeks tooget van hello Azure storage-account, Hallo volgende opdrachten uitvoeren:

* Lijst van alle opslagaccounts.

```bash
az storage account list -g iot-gateway --query [].name
```

* Azure-opslag-verbindingsreeks ophalen.

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

Gebruik `iot-gateway` als Hallo-waarde van `{resource group name}` als u Hallo-waarde in les 2 niet wijzigen.

## <a name="configure-hello-device-connection"></a>Hallo apparaatverbinding configureren

Update Hallo `config-azure.json` bestand zodat Hallo voorbeeldcode die wordt uitgevoerd op de hostcomputer Hallo bericht in uw Azure Table storage kan lezen. tooconfigure Hallo apparaatverbinding, als volgt te werk:

1. Open Hallo apparaat configuratiebestand `config-azure.json` door het uitvoeren van de volgende opdrachten Hallo:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![configuratie](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. Vervang `[Azure storage connection string]` Hello Azure storage-verbindingsreeks die u hebt verkregen.

   `[IoT hub connection string]`al in de sectie moet worden vervangen [berichten lezen uit Azure IoT Hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md) in Lesson3.

## <a name="read-messages-in-your-azure-table-storage"></a>Lezen van berichten in uw Azure-tabelopslag

Voer voorbeeldtoepassing Hallo-gateway en Azure Table storage berichten lezen door de volgende opdracht Hallo:

```bash
gulp run --table-storage
```

Uw IoT-hub geactiveerd toosave toepassingsbericht van uw Azure-functie in uw Azure-tabelopslag wanneer nieuw bericht binnenkomt.
Hallo `gulp run` opdracht wordt uitgevoerd voor gateway-voorbeeldtoepassing die berichten tooyour iothub verzendt. Met `table-storage` parameter, dit kan een onderliggend proces tooreceive Hallo-bericht opgeslagen in uw Azure-tabelopslag ook gestart.

Hallo-berichten die worden verzonden en ontvangen, worden alle weergegeven onmiddellijk op Hallo dezelfde consolevenster in Hallo hostmachine. Hallo voorbeeld toepassingsexemplaar wordt in 40 seconden automatisch beëindigd.

   ![gulp lezen](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table_simudev.png)


## <a name="summary"></a>Samenvatting

U hebt hello voorbeeld code tooread Hallo-berichten in uw Azure-tabelopslag opgeslagen door de toepassing van uw Azure-functie uitvoert.
