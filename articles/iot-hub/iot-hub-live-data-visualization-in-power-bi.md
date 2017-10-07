---
title: "aaaReal tijd gegevensvisualisatie van sensorgegevens uit Azure IoT Hub – Power BI | Microsoft Docs"
description: Gebruik Power BI toovisualize temperatuur en vochtigheid gegevens die worden verzameld van Hallo sensor en tooyour Azure IoT hub wordt verzonden.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: realtime gegevensvisualisatie, live gegevensvisualisatie, sensor gegevensvisualisatie
ms.assetid: e67c9c09-6219-4f0f-ad42-58edaaa74f61
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: d79ce757a9f2ab7a4744e8a0c523106e0f72cecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a>Realtime-sensorgegevens uit Azure IoT Hub met Power BI visualiseren

![End-to-end-diagram](media/iot-hub-get-started-e2e-diagram/4.png)


[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>Wat u leert

U leert hoe toovisualize realtime-sensorgegevens die uw Azure-IoT-hub ontvangt door Power BI. Als u wilt dat tootry Hallo gegevens visualiseren in uw iothub met Web-Apps, Zie [gebruik Azure Web Apps toovisualize realtime-sensorgegevens uit Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).

## <a name="what-you-do"></a>Wat u doet

- Bereid uw IoT-hub voor toegang tot gegevens door een consumergroep toe te voegen.
- Maken, configureren en uitvoeren van een Stream Analytics-taak voor overdracht van gegevens uit uw IoT hub tooyour Power BI-account.
- Maken en publiceren van een Power BI toovisualize Hallo rapportgegevens.

## <a name="what-you-need"></a>Wat u nodig hebt

- Zelfstudie [instellen van uw apparaat](iot-hub-raspberry-pi-kit-node-get-started.md) voltooid die Hallo volgens de vereisten worden behandeld:
  - Een actief Azure-abonnement.
  - Een Azure-IoT-hub in uw abonnement.
  - Een clienttoepassing die berichten tooyour Azure IoT hub verzendt.
- Een Power BI-account. ([Probeer Power BI gratis](https://powerbi.microsoft.com/))

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a>Maken, configureren en uitvoeren van een Stream Analytics-taak

### <a name="create-a-stream-analytics-job"></a>Een Stream Analytics-taak maken

1. In Azure-portal Hallo, klikt u op Nieuw > Internet der dingen > Stream Analytics-taak.
1. Voer Hallo informatie voor de taak hello te volgen.

   **Taaknaam**: Hallo-naam van Hallo-taak. Hallo-naam moet uniek zijn.

   **Resourcegroep**: gebruik Hallo dezelfde resourcegroep die gebruikmaakt van uw IoT-hub.

   **Locatie**: gebruik Hallo dezelfde locatie als de resourcegroep.

   **Pincode toodashboard**: Schakel deze optie voor eenvoudige toegang tooyour iothub uit het Hallo-dashboard.

   ![Een Stream Analytics-taak maken in Azure](media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

1. Klik op **Create**.

### <a name="add-an-input-toohello-stream-analytics-job"></a>Toevoegen van een invoer toohello Stream Analytics-taak

1. Open Hallo Stream Analytics-taak.
1. Onder **taak topologie**, klikt u op **invoer**.
1. In Hallo **invoer** deelvenster, klikt u op **toevoegen**, en voer de volgende informatie Hallo:

   **Invoeralias**: Hallo unieke alias voor Hallo-invoer.

   **Bron**: Selecteer **IoT-hub**.

   **Consumergroep**: Selecteer Hallo consumergroep u zojuist hebt gemaakt.
1. Klik op **Create**.

   ![Toevoegen van een invoer tooa Stream Analytics-taak in Azure](media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-toohello-stream-analytics-job"></a>Toevoegen van een uitvoer toohello Stream Analytics-taak

1. Onder **taak topologie**, klikt u op **uitvoer**.
1. In Hallo **uitvoer** deelvenster, klikt u op **toevoegen**, en voer de volgende informatie Hallo:

   **Uitvoeraliassen**: Hallo unieke alias voor Hallo uitvoer.

   **Sink**: Selecteer **Power BI**.
1. Klik op **autoriseren**, en vervolgens meldt u zich bij uw Power BI-account.
1. Na autorisatie, Voer Hallo volgende informatie:

   **Werkruimte groep**: Selecteer de groep doelwerkruimte.

   **Naam van DataSet**: Voer een gegevenssetnaam.

   **Tabelnaam**: Voer een tabelnaam.
1. Klik op **Create**.

   ![Een uitvoer tooa Stream Analytics-taak toevoegen in Azure](media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a>Hallo query van de Stream Analytics-taak Hallo configureren

1. Onder **taak topologie**, klikt u op **Query**.
1. Vervang `[YourInputAlias]` met alias van de taak Hallo Hallo invoer.
1. Vervang `[YourOutputAlias]` met Hallo uitvoeralias van Hallo-taak.
1. Klik op **Opslaan**.

   ![Een query tooa Stream Analytics-taak niet toevoegen in Azure](media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-hello-stream-analytics-job"></a>Hallo Stream Analytics-taak uitgevoerd

Klik in het Hallo-Stream Analytics-taak op **Start** > **nu** > **Start**. Zodra het Hallo-taak is gestart, Hallo taakstatus verandert van **gestopt** te**met**.

![Een Stream Analytics-taak uitgevoerd in Azure](media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-toovisualize-hello-data"></a>Maken en publiceren van een Power BI toovisualize Hallo rapportgegevens

1. Controleer de voorbeeldtoepassing hello wordt uitgevoerd op uw apparaat. Als u niet het geval is, raadpleegt u de zelfstudies toohello onder [instellen van uw apparaat](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).
1. Meld u aan tooyour [Power BI](https://powerbi.microsoft.com/en-us/) account.
1. Ga toohello groep werkruimte die u hebt ingesteld toen u Hallo uitvoer voor Hallo Stream Analytics-taak gemaakt.
1. Klik op **Streaming gegevenssets**.

   U ziet de gegevensset Hallo vermeld die u hebt opgegeven toen u Hallo uitvoer voor Hallo Stream Analytics-taak gemaakt.
1. Onder **acties**, klikt u op Hallo eerste pictogram toocreate een rapport.

   ![Een Microsoft Power BI-rapport maken](media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

1. Maak een regel grafiek tooshow realtime temperatuur gedurende een bepaalde periode.
   1. Voeg een lijndiagram op Hallo-rapportpagina maken.
   1. Op Hallo **velden** deelvenster Vouw Hallo tabel die u hebt opgegeven toen u Hallo uitvoer voor Hallo Stream Analytics-taak gemaakt.
   1. Sleep **EventEnqueuedUtcTime** te**as** op Hallo **visualisaties** deelvenster.
   1. Sleep **temperatuur** te**waarden**.

      Nu wordt een lijndiagram gemaakt. Hallo x-as geeft de datum en tijd in UTC-tijdzone Hallo. Hallo y-as worden temperatuur van Hallo sensor weergegeven.

      ![Toevoegen van een lijndiagram voor temperatuur tooa Microsoft Power BI-rapport](media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

1. Maak een andere regel grafiek tooshow realtime vochtigheid gedurende een bepaalde periode. toodo, volgt u dezelfde hierboven stappen Hallo op en plaats **EventEnqueuedUtcTime** op Hallo x-as en **vochtigheid** op Hallo y-as.

   ![Toevoegen van een lijndiagram voor vochtigheid tooa Microsoft Power BI-rapport](media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

1. Klik op **opslaan** toosave Hallo rapport.
1. Klik op **bestand** > **tooweb publiceren**.
1. Klik op **invoegcode maken**, en klik vervolgens op **publiceren**.

U bent Hallo rapportkoppeling die u met iemand voor toegang tot rapporten en een code codefragment toointegrate Hallo rapport in uw blog of website delen kunt opgegeven.

![Publiceren van een Microsoft Power BI-rapport](media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

Microsoft biedt ook Hallo [mobiele apps van Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) voor het weergeven en interactie met uw Power BI-dashboards en rapporten op je mobiele apparaat.

## <a name="next-steps"></a>Volgende stappen

U hebt Power BI toovisualize realtime-sensorgegevens met succes van uw Azure-IoT-hub gebruikt.
Er is een andere manier toovisualize-gegevens van Azure IoT Hub. Zie [gebruik Azure Web Apps toovisualize realtime-sensorgegevens uit Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
