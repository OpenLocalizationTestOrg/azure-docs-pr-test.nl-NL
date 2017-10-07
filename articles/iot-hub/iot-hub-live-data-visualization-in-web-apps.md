---
title: "aaaReal tijd gegevensvisualisatie van sensorgegevens uit uw Azure-IoT-hub – Web-Apps | Microsoft Docs"
description: Hallo-Web-Apps van Microsoft Azure App Service toovisualize temperatuur en vochtigheid gegevens die worden verzameld van Hallo sensor en verzonden tooyour Iot-hub gebruiken.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: realtime gegevensvisualisatie, live gegevensvisualisatie, sensor gegevensvisualisatie
ms.assetid: e42b07a8-ddd4-476e-9bfb-903d6b033e91
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 72f2dffee1c2f975948820eee9f2e287c3f77255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-your-azure-iot-hub-by-using-hello-web-apps-feature-of-azure-app-service"></a>Realtime-sensorgegevens uit uw Azure-IoT-hub visualiseren met behulp van de functie voor Hallo-Web-Apps van Azure App Service

![End-to-end-diagram](media/iot-hub-get-started-e2e-diagram/5.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>Wat u leert

In deze zelfstudie leert u hoe toovisualize realtime-sensorgegevens die uw IoT-hub ontvangt door het uitvoeren van een webtoepassing die wordt gehost op een web-app. Als u tootry toovisualize Hallo gegevens in uw iothub wilt met behulp van Power BI, Zie [gebruik Power BI toovisualize realtime-sensorgegevens uit Azure IoT Hub](iot-hub-live-data-visualization-in-power-bi.md).

## <a name="what-you-do"></a>Wat u doet

- Een web-app maken in hello Azure-portal.
- Bereid uw IoT-hub voor toegang tot gegevens door een consumergroep toe te voegen.
- Configureer Hallo web app tooread sensor-gegevens van uw IoT-hub.
- Een web application toobe gehost door Hallo web-app uploaden.
- Open Hallo web app toosee realtime temperatuur en vochtigheid gegevens uit uw IoT-hub.

## <a name="what-you-need"></a>Wat u nodig hebt

- [Instellen van uw apparaat](iot-hub-raspberry-pi-kit-node-get-started.md), die wordt ingegaan op Hallo volgens de vereisten:
  - Een actief Azure-abonnement
  - Een Iot-hub in uw abonnement
  - Een clienttoepassing die berichten tooyour Iot-hub verzendt
- [Git downloaden](https://www.git-scm.com/downloads)

## <a name="create-a-web-app"></a>Een webtoepassing maken

1. In Hallo [Azure-portal](https://ms.portal.azure.com/), klikt u op **nieuw** > **Web en mobiel** > **Web-App**.
2. Voer een unieke Taaknaam, Hallo abonnement controleren, Geef een resourcegroep en een locatie, selecteer **pincode toodashboard**, en klik vervolgens op **maken**.

   Het is raadzaam dat u Hallo selecteert dezelfde locatie bevinden als die van de resourcegroep. In dat geval helpt bij het verwerken van de snelheid en vermindert Hallo kosten voor gegevensoverdracht.

   ![Een webtoepassing maken](media/iot-hub-live-data-visualization-in-web-apps/2_create-web-app-azure.png)

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="configure-hello-web-app-tooread-data-from-your-iot-hub"></a>Hallo web app tooread-gegevens van uw IoT-hub configureren

1. Open Hallo-webtoepassing die u zojuist hebt ingericht.
2. Klik op **toepassingsinstellingen**, en klik vervolgens onder **appinstellingen**, toevoegen Hallo sleutel/waarde-paren te volgen:

   | Sleutel                                   | Waarde                                                        |
   |---------------------------------------|--------------------------------------------------------------|
   | Azure.IoT.IoTHub.ConnectionString     | Verkregen van iothub explorer                                |
   | Azure.IoT.IoTHub.ConsumerGroup        | Hallo-naam van consumentengroep hello tooyour IoT-hub toe te voegen  |

   ![Instellingen tooyour web-app met sleutel-waardeparen toevoegen](media/iot-hub-live-data-visualization-in-web-apps/4_web-app-settings-key-value-azure.png)

3. Klik op **toepassingsinstellingen**onder **algemene instellingen**, in-/ uitschakelen Hallo **Web-sockets** optie en klik vervolgens op **opslaan**.

   ![Stel Hallo Web sockets optie](media/iot-hub-live-data-visualization-in-web-apps/10_toggle_web_sockets.png)

## <a name="upload-a-web-application-toobe-hosted-by-hello-web-app"></a>Een web application toobe gehost door Hallo web-app uploaden

Op GitHub, hebben we aangebracht beschikbaar een webtoepassing die wordt weergegeven van realtime-sensorgegevens uit uw IoT-hub. Toodo hoeft u Hallo web app toowork configureren met een Git-opslagplaats en upload het tooAzure voor Hallo web app toohost Hallo webtoepassing vanuit GitHub downloaden.

1. Klik in het Hallo-web-app op **implementatieopties** > **bron kiezen** > **lokale Git-opslagplaats**, en klik vervolgens op **OK**.

   ![Configureren van uw web-app-implementatie toouse Hallo lokale Git-opslagplaats](media/iot-hub-live-data-visualization-in-web-apps/5_configure-web-app-deployment-local-git-repository-azure.png)

2. Klik op **Implementatiereferenties**, een gebruiker en het wachtwoord toouse tooconnect toohello Git-opslagplaats in Azure maken en klik vervolgens op **opslaan**.

3. Klik op **overzicht**, en bekijkt hello waarde **Git kloon-url**.

   ![Hallo Git kloon-URL van uw web-app ophalen](media/iot-hub-live-data-visualization-in-web-apps/7_web-app-git-clone-url-azure.png)

4. Open een opdracht of een terminalvenster op de lokale computer.

5. Hallo-web-app downloaden vanuit GitHub en upload het tooAzure voor Hallo web app toohost. toodo Voer dus Hallo volgende opdrachten:

   ```bash
   git clone https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization.git
   cd web-apps-node-iot-hub-data-visualization
   git remote add webapp <Git clone URL>
   git push webapp master:master
   ```

   > [!NOTE]
   > \<GIT kloon-URL\> Hallo-URL van Hallo Git-opslagplaats gevonden op Hallo **overzicht** pagina van Hallo web-app.

## <a name="open-hello-web-app-toosee-real-time-temperature-and-humidity-data-from-your-iot-hub"></a>Hallo web app toosee realtime temperatuur en vochtigheid gegevens openen vanuit uw IoT-hub

Op Hallo **overzicht** pagina van uw web-app klikt u op Hallo URL tooopen Hallo web-app.

![Hallo-URL van uw web-app ophalen](media/iot-hub-live-data-visualization-in-web-apps/8_web-app-url-azure.png)

U ziet Hallo realtime temperatuur en vochtigheid gegevens uit uw IoT-hub.

![Web-app-pagina met realtime temperatuur en vochtigheid](media/iot-hub-live-data-visualization-in-web-apps/9_web-app-page-show-real-time-temperature-humidity-azure.png)

> [!NOTE]
> Controleer de voorbeeldtoepassing hello wordt uitgevoerd op uw apparaat. Als dat niet zo is, ontvangt u een lege grafiek, raadpleegt u de zelfstudies toohello onder [instellen van uw apparaat](iot-hub-raspberry-pi-kit-node-get-started.md).

## <a name="next-steps"></a>Volgende stappen
U hebt uw web-app toovisualize realtime-sensorgegevens met succes van uw IoT-hub gebruikt.

Zie voor een andere manier toovisualize gegevens uit Azure IoT Hub, [gebruik Power BI toovisualize realtime-sensorgegevens uit uw IoT-hub](iot-hub-live-data-visualization-in-power-bi.md).

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
