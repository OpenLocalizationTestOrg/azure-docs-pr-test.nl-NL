---
title: aaaUnderstand hello Azure IoT Hub ingebouwd eindpunt | Microsoft Docs
description: Handleiding voor ontwikkelaars - hierin wordt beschreven hoe toouse Hallo ingebouwde Event Hub-compatibele eindpunt toread apparaat-naar-cloud-berichten.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 15484c1b1828151ffcae5f4a1407264374223da1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="read-device-to-cloud-messages-from-hello-built-in-endpoint"></a>Apparaat-naar-cloud-berichten lezen uit Hallo ingebouwd eindpunt

Berichten zijn standaard gerouteerde toohello ingebouwde gerichte service-eindpunt (**berichten/gebeurtenissen**), die compatibel is met [Event Hubs][lnk-event-hubs]. Dit eindpunt is momenteel alleen zichtbaar met Hallo [AMQP] [ lnk-amqp] -protocol op poort 5671. Een iothub toont Hallo na eigenschappen tooenable u toocontrol ingebouwde Event Hub-compatibele messaging eindpunt Hallo **berichten/gebeurtenissen**.

| Eigenschap            | Beschrijving |
| ------------------- | ----------- |
| **Aantal partities** | Stel deze eigenschap in op het maken van toodefine Hallo aantal [partities] [ lnk-event-hub-partitions] voor opname van apparaat-naar-cloud-gebeurtenis. |
| **Bewaartijd**  | Deze eigenschap specificeert hoe lang in dagen dat berichten door de IoT Hub worden bewaard. Hallo standaardwaarde is één dag, maar deze verhoogde tooseven dagen kan worden. |

IoT-Hub kunt u ook de consumergroepen toomanage op Hallo ingebouwde apparaat-naar-cloud eindpunt ontvangen.

Standaard worden alle berichten die niet expliciet overeen met een regel voor het doorsturen van bericht toohello ingebouwd eindpunt geschreven. Als u deze route voor terugval uitschakelt, worden berichten die niet expliciet overeen met alle regels voor het doorsturen van bericht verwijderd.

U kunt de bewaartijd hello, hetzij via een programma via Hallo wijzigen [resourceprovider IoT Hub REST-API's][lnk-resource-provider-apis], of met behulp van Hallo [Azure-portal] [ lnk-management-portal].

IoT-Hub toont Hallo **berichten/gebeurtenissen** ingebouwd eindpunt voor uw back-end services tooread hello apparaat-naar-cloud-berichten ontvangen door de hub. Dit eindpunt is Event Hub-compatibele, waarmee u toouse van Hallo mechanismen Hallo Event Hubs-service ondersteunt voor het lezen van berichten.

## <a name="read-from-hello-built-in-endpoint"></a>Lezen van de ingebouwde eindpunt Hallo

Wanneer u Hallo gebruikt [Azure Service Bus-SDK voor .NET] [ lnk-servicebus-sdk] of Hallo [Event Hubs - Gebeurtenisprocessorhost][lnk-eventprocessorhost], kunt u een IoT Hub-verbinding tekenreeksen met de juiste machtigingen Hallo. Gebruik vervolgens **berichten/gebeurtenissen** als Hallo Event Hub-naam.

Wanneer u SDK's (of product integraties) gebruikt die zich niet bewust zijn van IoT Hub, moet u een Event Hub-compatibele eindpunt en een Event Hub-compatibele naam ophalen uit Hallo Iothub-instellingen in Hallo [Azure-portal] [ lnk-management-portal]:

1. Klik op Hallo IoT hubblade **eindpunten**.
1. In Hallo **ingebouwde eindpunten** sectie, klikt u op **gebeurtenissen**. Hallo blade bevat Hallo volgende waarden: **Event Hub-compatibele eindpunt**, **Event Hub-compatibele naam**, **partities**, **bewaartijd**, en **consumergroepen**.

    ![Apparaat-naar-cloud-instellingen][img-eventhubcompatible]

Hallo IoT Hub SDK vereist Hallo eindpuntnaam IoT Hub, namelijk **berichten/gebeurtenissen** zoals weergegeven in Hallo **eindpunten** blade.

Als Hallo SDK die u moet een **hostnaam** of **Namespace** waarde, verwijdert u Hallo-schema uit Hallo **Event Hub-compatibele eindpunt**. Bijvoorbeeld, als uw Event Hub-compatibele eindpunt **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, Hallo **hostnaam** zou worden  **iothub ns-myiothub 1234.servicebus.windows.net**, en Hallo **Namespace** zou **iothub-ns-myiothub-1234**.

U kunt een beleid voor gedeelde toegang met Hallo **ServiceConnect** machtigingen tooconnect toohello opgegeven Event Hub.

Als u een Event Hub-verbindingsreeks toobuild moet met behulp van de vorige informatie hello, gebruikt u Hallo patroon volgen:

`Endpoint={Event Hub-compatible endpoint};SharedAccessKeyName={iot hub policy name};SharedAccessKey={iot hub policy key}`

Hallo-SDK's en integraties gebruikt die u kunt gebruiken met Event Hub-compatibele eindpunten die IoT-Hub toont bevat Hallo items in Hallo volgende lijst:

* [Java Event Hubs-client](https://github.com/hdinsight/eventhubs-client).
* [Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md). U kunt bekijken Hallo [spout bron](https://github.com/apache/storm/tree/master/external/storm-eventhubs) op GitHub.
* [Apache Spark-integratie](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over IoT-hubeindpunten [IoT-hubeindpunten][lnk-endpoints].

Hallo [aan de slag] [ lnk-get-started] zelfstudies ziet u hoe toosend apparaat-naar-cloud-berichten van de gesimuleerde apparaten en Hallo-berichten lezen uit Hallo ingebouwd eindpunt. Zie voor meer details Hallo [proces IoT Hub apparaat-naar-cloud-berichten met behulp van routes] [ lnk-d2c-tutorial] zelfstudie.

Als u wilt dat tooroute uw apparaat-naar-cloud-berichten toocustom eindpunten, Zie [berichtroutes en aangepaste eindpunten gebruikt voor apparaat-naar-cloud-berichten][lnk-custom].

[img-eventhubcompatible]: ./media/iot-hub-devguide-messages-read-builtin/eventhubcompatible.png

[lnk-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-get-started]: iot-hub-get-started.md
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-management-portal]: https://portal.azure.com
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-event-hub-partitions]: ../event-hubs/event-hubs-features.md#partitions
[lnk-servicebus-sdk]: https://www.nuget.org/packages/WindowsAzure.ServiceBus
[lnk-eventprocessorhost]: http://blogs.msdn.com/b/servicebus/archive/2015/01/16/event-processor-host-best-practices-part-1.aspx
[lnk-amqp]: https://www.amqp.org/
