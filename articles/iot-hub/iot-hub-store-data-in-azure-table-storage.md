---
title: aaaSave tooAzure gegevensopslag met berichten voor uw iothub | Microsoft Docs
description: Gebruik een Azure-functie app-toosave uw IoT hub berichten tooyour Azure-tabelopslag. Hallo IoT hub berichten bevatten informatie, zoals sensorgegevens dat wordt verzonden door uw IoT-apparaat.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: IOT-gegevensopslag, gegevensopslag iot-temperatuursensor
ms.assetid: 62fd14fd-aaaa-4b3d-8367-75c1111b6269
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: be72d9ba9a781822926364351b50f58f5d96e94a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="save-iot-hub-messages-that-contain-sensor-data-tooyour-azure-table-storage"></a>Opslaan van IoT hub berichten met sensor gegevens tooyour Azure-tabelopslag

![End-to-end-diagram](media/iot-hub-get-started-e2e-diagram/3.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>Wat u leert

U leert hoe werken app toostore IoT hub berichten in uw tabelopslag toocreate Azure storage-account en een Azure.

## <a name="what-you-do"></a>Wat u doet

- Een Azure-opslagaccount maken.
- Bereid uw IoT-hub verbindingsberichten tooread.
- Maken en implementeren van een Azure-functie-app.

## <a name="what-you-need"></a>Wat u nodig hebt

- [Instellen van uw apparaat](iot-hub-raspberry-pi-kit-node-get-started.md) toocover Hallo volgens de vereisten:
  - Een actief Azure-abonnement
  - Een IoT-hub in uw abonnement 
  - Een actieve toepassing waarmee berichten tooyour iothub worden verzonden

## <a name="create-an-azure-storage-account"></a>Een Azure-opslagaccount maken

1. In Hallo [Azure-portal](https://portal.azure.com/), klikt u op **nieuw** > **opslag** > **opslagaccount**  >   **Maak**.

2. Voer Hallo benodigde gegevens voor het Hallo-opslagaccount:

   ![Een opslagaccount maken in hello Azure-portal](media\iot-hub-store-data-in-azure-table-storage\1_azure-portal-create-storage-account.png)

   * **Naam**: Hallo-naam van Hallo-opslagaccount. Hallo-naam moet uniek zijn.

   * **Resourcegroep**: gebruik Hallo dezelfde resourcegroep die gebruikmaakt van uw IoT-hub.

   * **Pincode toodashboard**: Selecteer deze optie voor eenvoudige toegang tooyour iothub uit Hallo-dashboard.

3. Klik op **Create**.

## <a name="prepare-your-iot-hub-connection-tooread-messages"></a>Voorbereiden van uw IoT-hub tooread verbindingsberichten

IoT-hub toont een ingebouwde event hub-compatibele eindpunt tooenable toepassingen tooread IoT hub-berichten. Ondertussen toepassingen groepen tooread consumentgegevens uit uw IoT-hub gebruiken. Voordat u een Azure-functie app-tooread gegevens uit uw IoT-hub maakt, Hallo te volgen:

- De verbindingsreeks Hallo van uw IoT-hubeindpunt ophalen.
- Maak een consumergroep voor uw iothub.

### <a name="get-hello-connection-string-of-your-iot-hub-endpoint"></a>De verbindingsreeks Hallo van uw IoT-hubeindpunt ophalen

1. Open uw IoT-hub.

2. Op Hallo **IoT Hub** deelvenster onder **Messaging**, klikt u op **eindpunten**.

3. In Hallo rechtermuisknop deelvenster onder **ingebouwde eindpunten**, klikt u op **gebeurtenissen**.

4. In Hallo **eigenschappen** deelvenster, opmerking Hallo volgende waarden:
   - Event hub-compatibele eindpunt
   - Event hub-compatibele naam

   ![Ophalen van de verbindingsreeks Hallo van uw IoT-hubeindpunt in hello Azure-portal](media\iot-hub-store-data-in-azure-table-storage\2_azure-portal-iot-hub-endpoint-connection-string.png)

5. In Hallo **IoT Hub** deelvenster onder **instellingen**, klikt u op **gedeeld toegangsbeleid**.

6. Klik op **iothubowner**.

7. Opmerking Hallo **primaire sleutel** waarde.

8. De verbindingsreeks Hallo van uw IoT-hubeindpunt als volgt maken:

   `Endpoint=<Event Hub-compatible endpoint>;SharedAccessKeyName=iothubowner;SharedAccessKey=<Primary key>`

   > [!NOTE]
   > Vervang `<Event Hub-compatible endpoint>` en `<Primary key>` met Hallo-waarden die u eerder hebt genoteerd.

### <a name="create-a-consumer-group-for-your-iot-hub"></a>Een consumergroep voor uw iothub maken

1. Open uw IoT-hub.

2. In Hallo **IoT Hub** deelvenster onder **Messaging**, klikt u op **eindpunten**.

3. In Hallo rechtermuisknop deelvenster onder **ingebouwde eindpunten**, klikt u op **gebeurtenissen**.

4. In Hallo **eigenschappen** deelvenster onder **consumergroepen**, voer een naam en maak een notitie ervan.

5. Klik op **Opslaan**.

## <a name="create-and-deploy-an-azure-function-app"></a>Een Azure-functie-app maken en implementeren

1. In Hallo [Azure-portal](https://portal.azure.com/), klikt u op **nieuw** > **Compute** > **functie-App**  >   **Maak**.

2. Voer de vereiste gegevens Hallo voor Hallo functie-app.

   ![Een functie-app maken in hello Azure-portal](media\iot-hub-store-data-in-azure-table-storage\3_azure-portal-create-function-app.png)

   * **App-naam**: Hallo-naam van Hallo functie-app. Hallo-naam moet uniek zijn.

   * **Resourcegroep**: gebruik Hallo dezelfde resourcegroep die gebruikmaakt van uw IoT-hub.

   * **Storage-Account**: Hallo storage-account dat u hebt gemaakt.

   * **Pincode toodashboard**: Schakel deze optie voor eenvoudige toegang toohello functie-app vanuit Hallo-dashboard.

3. Klik op **Create**.

4. Na de Hallo functie-app is gemaakt, opent u het.

5. Maak een nieuwe functie door Hallo volgende te doen in Hallo-functie-app:

   a. Klik op **nieuwe functie**.

   b. Selecteer **JavaScript** voor **taal**, en **gegevensverwerking** voor **Scenario**.

   c. Klik op **maken van deze functie**, en klik vervolgens op **nieuwe functie**.

   d. Selecteer **JavaScript** voor Hallo-taal en **gegevensverwerking** voor Hallo scenario.

   e. Klik op Hallo **EventHubTrigger JavaScript** sjabloon.

   f. Voer de vereiste gegevens Hallo voor Hallo-sjabloon.

      * **Naam van de functie**: naam van de functie Hallo Hallo.

      * **Naam Event Hub**: Hallo event hub-compatibele naam die u eerder hebt genoteerd.

      * **Gebeurtenis-hubverbinding**: tooadd Hallo-verbindingsreeks van Hallo IoT-hubeindpunt die u hebt gemaakt, klikt u op **nieuw**.

   g. Klik op **Create**.

6. Uitvoer van de functie Hallo configureren door Hallo volgende te doen:

   a. Klik op **integreren** > **nieuwe uitvoer** > **Azure Table Storage** > **Selecteer**.

      ![Table storage tooyour functie-app toevoegen in hello Azure-portal](media\iot-hub-store-data-in-azure-table-storage\4_azure-portal-function-app-add-output-table-storage.png)

   b. Voer de vereiste gegevens Hallo.

      * **Parameter tabelnaam**: Gebruik `outputTable`, die wordt gebruikt in hello Azure van functie-code.
      
      * **Tabelnaam**: Gebruik `deviceData`.

      * **Storage-account verbinding**: klik op **nieuw**, en selecteer of Voer uw storage-account. Als het Hallo-storage-account niet wordt weergegeven, raadpleegt u [account opslagvereisten](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).
      
   c. Klik op **Opslaan**.

7. Onder **Triggers**, klikt u op **Azure Event Hub (eventHubMessages)**.

8. Onder **Event Hub consumergroep**, voer de naam Hallo van consumentengroep Hallo dat u maakte en klik vervolgens op **opslaan**.

9. Hallo-functie die u hebt gemaakt op Hallo links op en klik op **bestanden weergeven** op Hallo rechts.

10. Vervang de code Hallo in `index.js` door Hallo volgende:

   ```javascript
   'use strict';

   // This function is triggered each time a message is received in hello IoT hub.
   // hello message payload is persisted in an Azure storage table
 
   module.exports = function (context, iotHubMessage) {
    context.log('Message received: ' + JSON.stringify(iotHubMessage));
    var date = Date.now();
    var partitionKey = Math.floor(date / (24 * 60 * 60 * 1000)) + '';
    var rowKey = date + '';
    context.bindings.outputTable = {
     "partitionKey": partitionKey,
     "rowKey": rowKey,
     "message": JSON.stringify(iotHubMessage)
    };
    context.done();
   };
   ```

11. Klik op **Opslaan**.

U hebt nu Hallo functie-app gemaakt. Berichten die uw IoT-hub in tabelopslag ontvangt worden opgeslagen.

> [!NOTE]
> U kunt Hallo **uitvoeren** knop tootest Hallo functie-app. Wanneer u klikt op **uitvoeren**, test het Hallo-bericht tooyour iothub wordt verzonden. Hallo aankomst van het Hallo-bericht moet Hallo functie app toostart activeren en sla vervolgens Hallo-bericht tooyour tabelopslag. Hallo **logboeken** deelvenster Hallo details van Hallo proces vastgelegd.

## <a name="verify-your-message-in-your-table-storage"></a>Controleer of het bericht in de tabelopslag

1. Hallo-voorbeeldtoepassing uitvoeren op uw apparaat toosend berichten tooyour IoT-hub.

2. [Download en installeer Azure Opslagverkenner](http://storageexplorer.com/).

3. Open Opslagverkenner, klik op **een Azure-Account toevoegen** > **aanmelden**, en vervolgens weer aanmelden tooyour Azure-account.

4. Klik op uw Azure-abonnement > **Opslagaccounts** > uw storage-account > **tabellen** > **deviceData**.

   U ziet dat berichten worden verzonden van uw apparaat tooyour IoT-hub Hallo aangemeld `deviceData` tabel.

## <a name="next-steps"></a>Volgende stappen

U hebt gemaakt uw Azure storage-account en de Azure-functie-app, dat berichten worden opgeslagen die uw IoT-hub in de tabelopslag van uw ontvangt.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
