---
title: aaaIoT externe controle en meldingen met Azure Logic Apps | Microsoft Docs
description: Gebruik Azure Logic Apps voor IoT Temperatuurbewaking op uw IoT-hub en automatisch verzenden van meldingen tooyour postvak voor eventuele afwijkingen gedetecteerd.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: bewaking, iot-meldingen IOT iot Temperatuurbewaking
ms.assetid: 43043067-2e1f-42c9-953d-e2dce8fd86df
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 89396528ed63c37258e1b49f342f0723e686ecb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="iot-remote-monitoring-and-notifications-with-azure-logic-apps-connecting-your-iot-hub-and-mailbox"></a>Externe controle IoT en meldingen met Azure Logic Apps die gebruikmaken van uw IoT-hub en Postvak

![End-to-end-diagram](media/iot-hub-get-started-e2e-diagram/7.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

Logische Apps van Azure biedt een manier tooautomate processen als een reeks stappen. Een logische app kan verbinding maken tussen verschillende services en protocollen. Deze begint met een trigger, zoals 'Wanneer een account is toegevoegd', en gevolgd door een combinatie van acties zoals het verzenden van een pushmelding. Deze functie stelt Logic Apps een perfecte IoT-oplossing voor IoT bewaking, zoals de waarschuwing op afwijkingen is vereist, onder andere gebruiksscenario's bijwerkt.

## <a name="what-you-learn"></a>Wat u leert

U leert hoe toocreate een logische app die verbinding maakt van uw IoT-hub en uw postvak voor het controleren van de temperatuur en meldingen. Wanneer Hallo temperatuur hoger dan 30 C is, markeert voor client-toepassing hello `temperatureAlert = "true"` in Hallo-bericht van het tooyour iothub verzendt. Hallo-bericht triggers Hallo logic app toosend u een e-mailbericht.

## <a name="what-you-do"></a>Wat u doet

* Een service bus-naamruimte maken en toevoegen van een wachtrij tooit.
* Voeg een eindpunt en een routering regel tooyour IoT-hub.
* Maken, configureren en testen van een logische app.

## <a name="what-you-need"></a>Wat u nodig hebt

* Zelfstudie [instellen van uw apparaat](iot-hub-raspberry-pi-kit-node-get-started.md) voltooid die Hallo volgens de vereisten worden behandeld:
  * Een actief Azure-abonnement.
  * Een Azure-IoT-hub in uw abonnement.
  * Een clienttoepassing die berichten tooyour Azure IoT hub verzendt.

## <a name="create-service-bus-namespace-and-add-a-queue-tooit"></a>Service bus-naamruimte maken en toevoegen van een wachtrij tooit

### <a name="create-a-service-bus-namespace"></a>Een service bus-naamruimte maken

1. Op Hallo [Azure-portal](https://portal.azure.com/), klikt u op **nieuw** > **Enterprise Integration** > **Service Bus**.
1. Hallo volgende informatie bevatten:

   **Naam**: Hallo-naam van Hallo servicebus.

   **Prijscategorie**: klik op **Basic** > **Selecteer**. Hallo Basic laag is voldoende voor deze zelfstudie.

   **Resourcegroep**: gebruik Hallo dezelfde resourcegroep die gebruikmaakt van uw IoT-hub.

   **Locatie**: gebruik Hallo dezelfde locatie die gebruikmaakt van uw IoT-hub.
1. Klik op **Create**.

   ![Maken van een service bus-naamruimte in hello Azure-portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/1_create-service-bus-namespace-azure-portal.png)

### <a name="add-a-service-bus-queue"></a>Toevoegen van een service bus-wachtrij

1. Hallo service bus-naamruimte openen en klik vervolgens op **+ wachtrij**.
1. Voer een naam voor de wachtrij Hallo en klik vervolgens op **maken**.
1. Hallo service bus-wachtrij te openen en klik vervolgens op **gedeeld toegangsbeleid** > **+ toevoegen**.
1. Voer een naam voor het Hallo-beleid, selectievakje **beheren**, en klik vervolgens op **maken**.

   ![Toevoegen van een service bus-wachtrij in hello Azure-portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/2_add-service-bus-queue-azure-portal.png)

## <a name="add-an-endpoint-and-a-routing-rule-tooyour-iot-hub"></a>Voeg een eindpunt en een routering regel tooyour IoT-hub

### <a name="add-an-endpoint"></a>Een eindpunt toevoegen

1. Uw IoT-hub te openen, klikt u op eindpunten > + toevoegen.
1. Voer Hallo volgende informatie:

   **Naam**: Hallo-naam van het Hallo-eindpunt.

   **Eindpunttype**: Selecteer **Service Bus-wachtrij**.

   **Service Bus-naamruimte**: Selecteer Hallo-naamruimte die u hebt gemaakt.

   **Service Bus-wachtrij**: Selecteer Hallo wachtrij die u hebt gemaakt.
1. Klik op **OK**.

   ![Toevoegen van een eindpunt tooyour IoT-hub in hello Azure-portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/3_add-iot-hub-endpoint-azure-portal.png)

### <a name="add-a-routing-rule"></a>Toevoegen van een regel voor doorsturen

1. Klik op in uw IoT-hub **Routes** > **+ toevoegen**.
1. Voer Hallo volgende informatie:

   **Naam**: Hallo-naam van regel voor het doorsturen van Hallo.

   **Gegevensbron**: Selecteer **DeviceMessages**.

   **Eindpunt**: Selecteer Hallo eindpunt die u hebt gemaakt.

   **Querytekenreeks**: Voer `temperatureAlert = "true"`.
1. Klik op **Opslaan**.

   ![Toevoegen van een regel voor doorsturen in hello Azure-portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/4_add-routing-rule-azure-portal.png)

## <a name="create-and-configure-a-logic-app"></a>Maken en configureren van een logische app

### <a name="create-a-logic-app"></a>Een logische app maken

1. In Hallo [Azure-portal](https://portal.azure.com/), klikt u op **nieuw** > **Enterprise Integration** > **logische App**.
1. Voer Hallo volgende informatie:

   **Naam**: Hallo-naam van Hallo logische app.

   **Resourcegroep**: gebruik Hallo dezelfde resourcegroep die gebruikmaakt van uw IoT-hub.

   **Locatie**: gebruik Hallo dezelfde locatie die gebruikmaakt van uw IoT-hub.
1. Klik op **Create**.

### <a name="configure-hello-logic-app"></a>Hallo logic app configureren

1. Hallo logische app dat wordt geopend in Hallo Logic Apps Designer openen.
1. In Hallo Logic Apps Designer, klikt u op **lege logische App**.

   ![Beginnen met een lege logische app in hello Azure-portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/5_start-with-blank-logic-app-azure-portal.png)

1. Klik op **Service Bus**.

   ![Selecteer de Service Bus toostart uw logische app maken in hello Azure-portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/6_select-service-bus-when-creating-blank-logic-app-azure-portal.png)

1. Klik op **Service Bus-bij een of meer in een wachtrij (automatisch aanvullen berichten)**.
1. Een service bus-verbinding maken.
   1. Voer een verbindingsnaam.
   1. Klik op service bus-naamruimte Hallo > Hallo service bus-beleid > **maken**.

      ![Een service bus-verbinding voor uw logische app maken in hello Azure-portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/7_create-service-bus-connection-in-logic-app-azure-portal.png)

   1. Klik op **doorgaan** nadat Hallo service bus-verbinding is gemaakt.
   1. Selecteer Hallo wachtrij die u hebt gemaakt en voer `175` voor **maximumaantal bericht**

      ![Hallo maximale aantal voor Hallo service bus-verbinding in uw logische app opgeven](media/iot-hub-monitoring-notifications-with-azure-logic-apps/8_specify-maximum-message-count-for-service-bus-connection-logic-app-azure-portal.png)
   1. Klik op knop toosave Hallo wijzigingen ' opgeslagen'.

1. Maak een SMTP-service-verbinding.
   1. Klik op **nieuwe stap** > **een actie toevoegen**.
   1. Type `SMTP`, klikt u op Hallo **SMTP** service in de zoekresultaten Hallo en klik vervolgens op **SMTP - e-mailbericht verzenden**.

      ![Een SMTP-verbinding maken in uw logische app in hello Azure-portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/9_create-smtp-connection-logic-app-azure-portal.png)

   1. Voer Hallo SMTP-gegevens van uw postvak in en klik vervolgens op **maken**.

      ![Voer SMTP-verbindingsgegevens in uw logische app in hello Azure-portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/10_enter-smtp-connection-info-logic-app-azure-portal.png)

      Hallo SMTP-informatie ophalen voor [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), en [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).
   1. Voer uw e-mailadres voor **van** en **naar**, en `High temperature detected` voor **onderwerp** en **hoofdtekst**.
   1. Klik op **Opslaan**.

Hallo logische app is defect wanneer u deze opslaat.

## <a name="test-hello-logic-app"></a>Test Hallo logische app

1. Hallo-clienttoepassing die u implementeert tooyour apparaat in Start [ESP8266 verbinding tooAzure IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md).
1. Hallo omgeving temperatuur rond Hallo SensorTag toobe hierboven 30 C. verhogen Bijvoorbeeld, een kaars rond de SensorTag lichten.
1. U ontvangt een e-mailmelding verzonden door Hallo logische app.

   > [!NOTE]
   > Uw e-provider moet mogelijk tooverify Hallo afzender identiteit toomake afbeelding moet u die Hallo e-mailbericht verzendt.

## <a name="next-steps"></a>Volgende stappen

U hebt gemaakt aan een logische app die verbinding maakt van uw IoT-hub en uw postvak voor het controleren van de temperatuur en meldingen.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
