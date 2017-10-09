---
title: aaaWeather prognose met Azure Machine Learning met gegevens uit IoT Hub | Microsoft Docs
description: Azure Machine Learning regen toopredict Hallo kans op basis van Hallo temperatuur en vochtigheid gegevens die uw IoT-hub worden verzameld van een sensor gebruiken.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: prognose weer machine learning
ms.assetid: 8ba7d9e7-699c-4448-b353-0f3e1429d198
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 04abe97558ccfc152bae2e0d435033433c0023dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="weather-forecast-using-hello-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a>Weer voor de prognose met Hallo sensorgegevens uit uw IoT-hub in Azure Machine Learning

![End-to-end-diagram](media/iot-hub-get-started-e2e-diagram/6.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

Machine learning is een techniek voor gegevenswetenschap waarmee computers leren van bestaande gegevens tooforecast toekomstig gedrag, resultaten en trends. Azure Machine Learning is een cloudservice voor predictive analytics waarmee u mogelijke tooquickly kunt maken en implementeren van voorspellende modellen als analytics-oplossingen.

## <a name="what-you-learn"></a>Wat u leert

U leert hoe toouse Azure Machine Learning toodo weer prognose (kans regen) met behulp van Hallo temperatuur en vochtigheid gegevens van uw Azure-IoT-hub. Hallo kans regen is Hallo-uitvoer van een model van de voorspelling voorbereide weer. Hallo-model is gebaseerd op historische gegevens tooforecast kans regen op basis van temperatuur en vochtigheid.

## <a name="what-you-do"></a>Wat u doet

- Hallo weer voorspellingsmodel implementeren als een webservice.
- Bereid uw IoT-hub voor toegang tot gegevens door een consumergroep toe te voegen.
- Een Stream Analytics-taak maken en Hallo taak te configureren:
  - Temperatuur en vochtigheid gegevens lezen uit uw IoT-hub.
  - Hallo web service tooget Hallo regen kans aanroepen.
  - Sla Hallo resultaat tooan Azure blob-opslag.
- Microsoft Azure Storage Explorer tooview Hallo weer prognose gebruiken.

## <a name="what-you-need"></a>Wat u nodig hebt

- Zelfstudie [instellen van uw apparaat](iot-hub-raspberry-pi-kit-node-get-started.md) voltooid die Hallo volgens de vereisten worden behandeld:
  - Een actief Azure-abonnement.
  - Een Azure-IoT-hub in uw abonnement.
  - Een clienttoepassing die berichten tooyour Azure IoT hub verzendt.
- Een Azure Machine Learning Studio-account. ([Machine Learning Studio gratis proberen](https://studio.azureml.net/)).

## <a name="deploy-hello-weather-prediction-model-as-a-web-service"></a>Hallo weer voorspellingsmodel als een webservice implementeren

1. Ga toohello [weer voorspelling modelpagina](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).
1. Klik op **openen in Studio** in Microsoft Azure Machine Learning Studio.
   ![Open Hallo weer voorspelling modelpagina in Cortana Intelligence Gallery](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)
1. Klik op **uitvoeren** toovalidate Hallo stappen voor het Hallo-model. Deze stap kan toocomplete 2 minuten duren.
   ![Open Hallo weer voorspellingsmodel in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)
1. Klik op **instellen van WEBSERVICE** > **voorspellende webservice**.
   ![Hallo weer voorspellingsmodel in Azure Machine Learning Studio implementeren](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)
1. Sleep in Hallo diagram Hallo **Web service invoer** module ergens in de buurt van Hallo **Score Model** module.
1. Verbinding maken met de Hallo **Web service invoer** module toohello **Score Model** module.
   ![Verbinding maken met twee modules in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)
1. Klik op **uitvoeren** toovalidate Hallo stappen voor het Hallo-model.
1. Klik op **WEBSERVICE implementeren** toodeploy Hallo model als een webservice.
1. Op Hallo dashboard van Hallo-model downloaden Hallo **Excel 2010 of ouder werkmap** voor **aanvraag/antwoord**.

   > [!Note]
   > Zorg ervoor dat u Hallo downloaden **Excel 2010 of ouder werkmap** zelfs als u een nieuwere versie van Excel worden uitgevoerd op uw computer.

   ![Hallo Excel voor Hallo REQUEST RESPONSE-eindpunt downloaden](media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. Hallo Excel-werkmap opent, noteer Hallo **URL van WEBSERVICE** en **TOEGANGSSLEUTEL**.

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a>Maken, configureren en uitvoeren van een Stream Analytics-taak

### <a name="create-a-stream-analytics-job"></a>Een Stream Analytics-taak maken

1. In Hallo [Azure-portal](https://ms.portal.azure.com/), klikt u op **nieuw** > **Internet der dingen** > **Stream Analytics-taak**.
1. Voer Hallo informatie voor de taak hello te volgen.

   **Taaknaam**: Hallo-naam van Hallo-taak. Hallo-naam moet uniek zijn.

   **Resourcegroep**: gebruik Hallo dezelfde resourcegroep die gebruikmaakt van uw IoT-hub.

   **Locatie**: gebruik Hallo dezelfde locatie als de resourcegroep.

   **Pincode toodashboard**: Schakel deze optie voor eenvoudige toegang tooyour iothub uit het Hallo-dashboard.

   ![Een Stream Analytics-taak maken in Azure](media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. Klik op **Create**.

### <a name="add-an-input-toohello-stream-analytics-job"></a>Toevoegen van een invoer toohello Stream Analytics-taak

1. Open Hallo Stream Analytics-taak.
1. Onder **taak topologie**, klikt u op **invoer**.
1. In Hallo **invoer** deelvenster, klikt u op **toevoegen**, en voer de volgende informatie Hallo:

   **Invoeralias**: Hallo unieke alias voor Hallo-invoer.

   **Bron**: Selecteer **IoT-hub**.

   **Consumergroep**: Selecteer Hallo consumergroep u hebt gemaakt.

   ![Toevoegen van een invoer toohello Stream Analytics-taak in Azure](media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. Klik op **Create**.

### <a name="add-an-output-toohello-stream-analytics-job"></a>Toevoegen van een uitvoer toohello Stream Analytics-taak

1. Onder **taak topologie**, klikt u op **uitvoer**.
1. In Hallo **uitvoer** deelvenster, klikt u op **toevoegen**, en voer de volgende informatie Hallo:

   **Uitvoeraliassen**: Hallo unieke alias voor Hallo uitvoer.

   **Sink**: Selecteer **Blob Storage**.

   **Storage-account**: Hallo storage-account voor de blob-opslag. U kunt een opslagaccount maken of een bestaande gebruiken.

   **Container**: Hallo container waarin Hallo blob is opgeslagen. U kunt een container maken of een bestaande gebruiken.

   **Gebeurtenis serialisatie-indeling**: Selecteer **CSV**.

   ![Een uitvoer toohello Stream Analytics-taak toevoegen in Azure](media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. Klik op **Create**.

### <a name="add-a-function-toohello-stream-analytics-job-toocall-hello-web-service-you-deployed"></a>Een functie toohello Stream Analytics-taak toocall Hallo u geïmplementeerde webservice toevoegen

1. Onder **taak topologie**, klikt u op **functies** > **toevoegen**.
1. Voer Hallo volgende informatie:

   **Functie Alias**: Voer `machinelearning`.

   **Type functie**: Selecteer **Azure ML**.

   **Optie importeren**: Selecteer **importeren uit een ander abonnement**.

   **URL**: Voer Hallo WEBSERVICE-URL die u hebt genoteerd omlaag van Hallo Excel-werkmap.

   **Sleutel**: Voer Hallo TOEGANGSSLEUTEL die u hebt genoteerd omlaag van Hallo Excel-werkmap.

   ![Een functie toohello Stream Analytics-taak niet toevoegen in Azure](media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. Klik op **Create**.

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a>Hallo query van de Stream Analytics-taak Hallo configureren

1. Onder **taak topologie**, klikt u op **Query**.
1. De bestaande code Hallo vervangen door Hallo code te volgen:

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   Vervang `[YourInputAlias]` met alias van de taak Hallo Hallo invoer.

   Vervang `[YourOutputAlias]` met Hallo uitvoeralias van Hallo-taak.

1. Klik op **Opslaan**.

### <a name="run-hello-stream-analytics-job"></a>Hallo Stream Analytics-taak uitgevoerd

Klik in het Hallo-Stream Analytics-taak op **Start** > **nu** > **Start**. Zodra het Hallo-taak is gestart, Hallo taakstatus verandert van **gestopt** te**met**.

![Hallo Stream Analytics-taak uitgevoerd](media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-tooview-hello-weather-forecast"></a>Microsoft Azure Storage Explorer tooview Hallo weer prognose gebruiken

Voer Hallo client toepassing toostart verzamelen en verzenden van temperatuur en vochtigheid gegevens tooyour IoT-hub. Voor elk bericht dat uw IoT-hub ontvangt, roept Hallo Stream Analytics-taak Hallo weer prognose web service tooproduce Hallo kans regen. Hallo resultaat wordt vervolgens opgeslagen tooyour Azure blob-opslag. Azure Storage Explorer is een hulpprogramma waarmee u tooview Hallo resultaat kunt.

1. [Download en installeer Microsoft Azure Storage Explorer](http://storageexplorer.com/).
1. Open Azure Opslagverkenner.
1. Meld u aan tooyour Azure-account.
1. Selecteer uw abonnement.
1. Klik op uw abonnement > **Opslagaccounts** > uw storage-account > **Blob-Containers** > uw container.
1. Open een .csv-bestand toosee Hallo resultaat. de laatste kolom records Hallo Hallo kans regen.

   ![Resultaat van de prognose weer met Azure Machine Learning](media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a>Samenvatting

U hebt Azure Machine Learning tooproduce Hallo kans op basis van Hallo temperatuur en vochtigheid gegevens die uw IoT-hub ontvangt regen is gebruikt.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]