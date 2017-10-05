---
title: 'Gesimuleerde apparaat & Azure IoT Gateway - les 4: Table storage | Microsoft Docs'
description: Intel NUC berichten opslaan op uw IoT-hub, geschreven naar Azure Table storage en ze vervolgens vanuit de cloud te lezen.
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
ms.openlocfilehash: de5fae794c195132e2a487c0095845c756aa28e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a>Alleen berichten permanent in Azure Table storage

## <a name="what-you-will-do"></a>Wat u doet

- De voorbeeldtoepassing gateway uitvoeren op uw gateway dat berichten naar uw IoT-hub verzendt.
- Voorbeeldcode uitvoeren op de hostcomputer lezen van berichten in uw Azure Table-opslag.

Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Wat u leert

Het gebruik van het hulpprogramma gulp de voorbeeldcode om te lezen van berichten in uw Azure-tabelopslag uitvoeren.

## <a name="what-you-need"></a>Wat u nodig hebt

U hebt met succes uitgevoerd de volgende taken:

- [De functie Azure-app en de Azure storage-account gemaakt](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md).
- [Uitvoeren van de voorbeeldtoepassing gateway](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).
- [Lezen van berichten uit uw IoT-hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md).

## <a name="get-your-azure-storage-connection-strings"></a>Uw Azure storage-verbindingsreeksen ophalen

In deze les vroeg u een Azure storage-account gemaakt. Als u de verbindingsreeks van de Azure storage-account, voer de volgende opdrachten:

* Lijst van alle opslagaccounts.

```bash
az storage account list -g iot-gateway --query [].name
```

* Azure-opslag-verbindingsreeks ophalen.

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

Gebruik `iot-gateway` als de waarde van `{resource group name}` als u de waarde in les 2 is niet gewijzigd.

## <a name="configure-the-device-connection"></a>De apparaatverbinding configureren

Update de `config-azure.json` bestand zodat de voorbeeldcode die wordt uitgevoerd op de computer in uw Azure-tabelopslag bericht kan lezen. Volg deze stappen voor het configureren van de apparaatverbinding:

1. Open het configuratiebestand van het apparaat `config-azure.json` met de volgende opdrachten:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![configuratie](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. Vervang `[Azure storage connection string]` met de verbindingsreeks voor Azure-opslag die u hebt verkregen.

   `[IoT hub connection string]`al in de sectie moet worden vervangen [berichten lezen uit Azure IoT Hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md) in Lesson3.

## <a name="read-messages-in-your-azure-table-storage"></a>Lezen van berichten in uw Azure-tabelopslag

Voer de voorbeeldtoepassing gateway en Azure Table storage berichten gelezen door de volgende opdracht:

```bash
gulp run --table-storage
```

Uw IoT-hub wordt geactiveerd voor uw toepassing Azure-functie in het bericht in uw Azure-tabelopslag op te slaan wanneer nieuw bericht binnenkomt.
De `gulp run` opdracht wordt uitgevoerd voor gateway-voorbeeldtoepassing die berichten naar uw IoT-hub verzendt. Met `table-storage` parameter, dit kan een onderliggend proces voor het ontvangen van het bericht opgeslagen in uw Azure-tabelopslag ook gestart.

De berichten die worden verzonden en ontvangen, worden alle weergegeven onmiddellijk op de dezelfde consolevenster in de hostmachine. Het exemplaar van de steekproef wordt beëindigd automatisch op 40 seconden.

   ![gulp lezen](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table_simudev.png)


## <a name="summary"></a>Samenvatting

U kunt de voorbeeldcode om te lezen van de berichten in uw Azure-tabelopslag opgeslagen door de toepassing van uw Azure-functie hebt uitgevoerd.
