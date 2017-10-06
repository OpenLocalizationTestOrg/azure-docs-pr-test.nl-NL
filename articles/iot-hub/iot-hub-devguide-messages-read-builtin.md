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
# <a name="read-device-to-cloud-messages-from-hello-built-in-endpoint"></a><span data-ttu-id="a2a25-103">Apparaat-naar-cloud-berichten lezen uit Hallo ingebouwd eindpunt</span><span class="sxs-lookup"><span data-stu-id="a2a25-103">Read device-to-cloud messages from hello built-in endpoint</span></span>

<span data-ttu-id="a2a25-104">Berichten zijn standaard gerouteerde toohello ingebouwde gerichte service-eindpunt (**berichten/gebeurtenissen**), die compatibel is met [Event Hubs][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="a2a25-104">By default, messages are routed toohello built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="a2a25-105">Dit eindpunt is momenteel alleen zichtbaar met Hallo [AMQP] [ lnk-amqp] -protocol op poort 5671.</span><span class="sxs-lookup"><span data-stu-id="a2a25-105">This endpoint is currently only exposed using hello [AMQP][lnk-amqp] protocol on port 5671.</span></span> <span data-ttu-id="a2a25-106">Een iothub toont Hallo na eigenschappen tooenable u toocontrol ingebouwde Event Hub-compatibele messaging eindpunt Hallo **berichten/gebeurtenissen**.</span><span class="sxs-lookup"><span data-stu-id="a2a25-106">An IoT hub exposes hello following properties tooenable you toocontrol hello built-in Event Hub-compatible messaging endpoint **messages/events**.</span></span>

| <span data-ttu-id="a2a25-107">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="a2a25-107">Property</span></span>            | <span data-ttu-id="a2a25-108">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a2a25-108">Description</span></span> |
| ------------------- | ----------- |
| <span data-ttu-id="a2a25-109">**Aantal partities**</span><span class="sxs-lookup"><span data-stu-id="a2a25-109">**Partition count**</span></span> | <span data-ttu-id="a2a25-110">Stel deze eigenschap in op het maken van toodefine Hallo aantal [partities] [ lnk-event-hub-partitions] voor opname van apparaat-naar-cloud-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="a2a25-110">Set this property at creation toodefine hello number of [partitions][lnk-event-hub-partitions] for device-to-cloud event ingestion.</span></span> |
| <span data-ttu-id="a2a25-111">**Bewaartijd**</span><span class="sxs-lookup"><span data-stu-id="a2a25-111">**Retention time**</span></span>  | <span data-ttu-id="a2a25-112">Deze eigenschap specificeert hoe lang in dagen dat berichten door de IoT Hub worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="a2a25-112">This property specifies how long in days messages are retained by IoT Hub.</span></span> <span data-ttu-id="a2a25-113">Hallo standaardwaarde is één dag, maar deze verhoogde tooseven dagen kan worden.</span><span class="sxs-lookup"><span data-stu-id="a2a25-113">hello default is one day, but it can be increased tooseven days.</span></span> |

<span data-ttu-id="a2a25-114">IoT-Hub kunt u ook de consumergroepen toomanage op Hallo ingebouwde apparaat-naar-cloud eindpunt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="a2a25-114">IoT Hub also enables you toomanage consumer groups on hello built-in device-to-cloud receive endpoint.</span></span>

<span data-ttu-id="a2a25-115">Standaard worden alle berichten die niet expliciet overeen met een regel voor het doorsturen van bericht toohello ingebouwd eindpunt geschreven.</span><span class="sxs-lookup"><span data-stu-id="a2a25-115">By default, all messages that do not explicitly match a message routing rule are written toohello built-in endpoint.</span></span> <span data-ttu-id="a2a25-116">Als u deze route voor terugval uitschakelt, worden berichten die niet expliciet overeen met alle regels voor het doorsturen van bericht verwijderd.</span><span class="sxs-lookup"><span data-stu-id="a2a25-116">If you disable this fallback route, messages that do not explicitly match any message routing rules are dropped.</span></span>

<span data-ttu-id="a2a25-117">U kunt de bewaartijd hello, hetzij via een programma via Hallo wijzigen [resourceprovider IoT Hub REST-API's][lnk-resource-provider-apis], of met behulp van Hallo [Azure-portal] [ lnk-management-portal].</span><span class="sxs-lookup"><span data-stu-id="a2a25-117">You can modify hello retention time, either programmatically through hello [IoT Hub resource provider REST APIs][lnk-resource-provider-apis], or by using hello [Azure portal][lnk-management-portal].</span></span>

<span data-ttu-id="a2a25-118">IoT-Hub toont Hallo **berichten/gebeurtenissen** ingebouwd eindpunt voor uw back-end services tooread hello apparaat-naar-cloud-berichten ontvangen door de hub.</span><span class="sxs-lookup"><span data-stu-id="a2a25-118">IoT Hub exposes hello **messages/events** built-in endpoint for your back-end services tooread hello device-to-cloud messages received by your hub.</span></span> <span data-ttu-id="a2a25-119">Dit eindpunt is Event Hub-compatibele, waarmee u toouse van Hallo mechanismen Hallo Event Hubs-service ondersteunt voor het lezen van berichten.</span><span class="sxs-lookup"><span data-stu-id="a2a25-119">This endpoint is Event Hub-compatible, which enables you toouse any of hello mechanisms hello Event Hubs service supports for reading messages.</span></span>

## <a name="read-from-hello-built-in-endpoint"></a><span data-ttu-id="a2a25-120">Lezen van de ingebouwde eindpunt Hallo</span><span class="sxs-lookup"><span data-stu-id="a2a25-120">Read from hello built-in endpoint</span></span>

<span data-ttu-id="a2a25-121">Wanneer u Hallo gebruikt [Azure Service Bus-SDK voor .NET] [ lnk-servicebus-sdk] of Hallo [Event Hubs - Gebeurtenisprocessorhost][lnk-eventprocessorhost], kunt u een IoT Hub-verbinding tekenreeksen met de juiste machtigingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="a2a25-121">When you use hello [Azure Service Bus SDK for .NET][lnk-servicebus-sdk] or hello [Event Hubs - Event Processor Host][lnk-eventprocessorhost], you can use any IoT Hub connection strings with hello correct permissions.</span></span> <span data-ttu-id="a2a25-122">Gebruik vervolgens **berichten/gebeurtenissen** als Hallo Event Hub-naam.</span><span class="sxs-lookup"><span data-stu-id="a2a25-122">Then use **messages/events** as hello Event Hub name.</span></span>

<span data-ttu-id="a2a25-123">Wanneer u SDK's (of product integraties) gebruikt die zich niet bewust zijn van IoT Hub, moet u een Event Hub-compatibele eindpunt en een Event Hub-compatibele naam ophalen uit Hallo Iothub-instellingen in Hallo [Azure-portal] [ lnk-management-portal]:</span><span class="sxs-lookup"><span data-stu-id="a2a25-123">When you use SDKs (or product integrations) that are unaware of IoT Hub, you must retrieve an Event Hub-compatible endpoint and Event Hub-compatible name from hello IoT Hub settings in hello [Azure portal][lnk-management-portal]:</span></span>

1. <span data-ttu-id="a2a25-124">Klik op Hallo IoT hubblade **eindpunten**.</span><span class="sxs-lookup"><span data-stu-id="a2a25-124">In hello IoT hub blade, click **Endpoints**.</span></span>
1. <span data-ttu-id="a2a25-125">In Hallo **ingebouwde eindpunten** sectie, klikt u op **gebeurtenissen**.</span><span class="sxs-lookup"><span data-stu-id="a2a25-125">In hello **Built-in endpoints** section, click **Events**.</span></span> <span data-ttu-id="a2a25-126">Hallo blade bevat Hallo volgende waarden: **Event Hub-compatibele eindpunt**, **Event Hub-compatibele naam**, **partities**, **bewaartijd**, en **consumergroepen**.</span><span class="sxs-lookup"><span data-stu-id="a2a25-126">hello blade contains hello following values: **Event Hub-compatible endpoint**, **Event Hub-compatible name**, **Partitions**, **Retention time**, and **Consumer groups**.</span></span>

    ![Apparaat-naar-cloud-instellingen][img-eventhubcompatible]

<span data-ttu-id="a2a25-128">Hallo IoT Hub SDK vereist Hallo eindpuntnaam IoT Hub, namelijk **berichten/gebeurtenissen** zoals weergegeven in Hallo **eindpunten** blade.</span><span class="sxs-lookup"><span data-stu-id="a2a25-128">hello IoT Hub SDK requires hello IoT Hub endpoint name, which is **messages/events** as shown in hello **Endpoints** blade.</span></span>

<span data-ttu-id="a2a25-129">Als Hallo SDK die u moet een **hostnaam** of **Namespace** waarde, verwijdert u Hallo-schema uit Hallo **Event Hub-compatibele eindpunt**.</span><span class="sxs-lookup"><span data-stu-id="a2a25-129">If hello SDK you are using requires a **Hostname** or **Namespace** value, remove hello scheme from hello **Event Hub-compatible endpoint**.</span></span> <span data-ttu-id="a2a25-130">Bijvoorbeeld, als uw Event Hub-compatibele eindpunt **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, Hallo **hostnaam** zou worden  **iothub ns-myiothub 1234.servicebus.windows.net**, en Hallo **Namespace** zou **iothub-ns-myiothub-1234**.</span><span class="sxs-lookup"><span data-stu-id="a2a25-130">For example, if your Event Hub-compatible endpoint is **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, hello **Hostname** would be **iothub-ns-myiothub-1234.servicebus.windows.net**, and hello **Namespace** would be **iothub-ns-myiothub-1234**.</span></span>

<span data-ttu-id="a2a25-131">U kunt een beleid voor gedeelde toegang met Hallo **ServiceConnect** machtigingen tooconnect toohello opgegeven Event Hub.</span><span class="sxs-lookup"><span data-stu-id="a2a25-131">You can then use any shared access policy that has hello **ServiceConnect** permissions tooconnect toohello specified Event Hub.</span></span>

<span data-ttu-id="a2a25-132">Als u een Event Hub-verbindingsreeks toobuild moet met behulp van de vorige informatie hello, gebruikt u Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="a2a25-132">If you need toobuild an Event Hub connection string by using hello previous information, use hello following pattern:</span></span>

`Endpoint={Event Hub-compatible endpoint};SharedAccessKeyName={iot hub policy name};SharedAccessKey={iot hub policy key}`

<span data-ttu-id="a2a25-133">Hallo-SDK's en integraties gebruikt die u kunt gebruiken met Event Hub-compatibele eindpunten die IoT-Hub toont bevat Hallo items in Hallo volgende lijst:</span><span class="sxs-lookup"><span data-stu-id="a2a25-133">hello SDKs and integrations that you can use with Event Hub-compatible endpoints that IoT Hub exposes includes hello items in hello following list:</span></span>

* <span data-ttu-id="a2a25-134">[Java Event Hubs-client](https://github.com/hdinsight/eventhubs-client).</span><span class="sxs-lookup"><span data-stu-id="a2a25-134">[Java Event Hubs client](https://github.com/hdinsight/eventhubs-client).</span></span>
* <span data-ttu-id="a2a25-135">[Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="a2a25-135">[Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span> <span data-ttu-id="a2a25-136">U kunt bekijken Hallo [spout bron](https://github.com/apache/storm/tree/master/external/storm-eventhubs) op GitHub.</span><span class="sxs-lookup"><span data-stu-id="a2a25-136">You can view hello [spout source](https://github.com/apache/storm/tree/master/external/storm-eventhubs) on GitHub.</span></span>
* <span data-ttu-id="a2a25-137">[Apache Spark-integratie](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span><span class="sxs-lookup"><span data-stu-id="a2a25-137">[Apache Spark integration](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2a25-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a2a25-138">Next steps</span></span>

<span data-ttu-id="a2a25-139">Zie voor meer informatie over IoT-hubeindpunten [IoT-hubeindpunten][lnk-endpoints].</span><span class="sxs-lookup"><span data-stu-id="a2a25-139">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-endpoints].</span></span>

<span data-ttu-id="a2a25-140">Hallo [aan de slag] [ lnk-get-started] zelfstudies ziet u hoe toosend apparaat-naar-cloud-berichten van de gesimuleerde apparaten en Hallo-berichten lezen uit Hallo ingebouwd eindpunt.</span><span class="sxs-lookup"><span data-stu-id="a2a25-140">hello [Get Started][lnk-get-started] tutorials show you how toosend device-to-cloud messages from simulated devices and read hello messages from hello built-in endpoint.</span></span> <span data-ttu-id="a2a25-141">Zie voor meer details Hallo [proces IoT Hub apparaat-naar-cloud-berichten met behulp van routes] [ lnk-d2c-tutorial] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="a2a25-141">For more detail, see hello [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

<span data-ttu-id="a2a25-142">Als u wilt dat tooroute uw apparaat-naar-cloud-berichten toocustom eindpunten, Zie [berichtroutes en aangepaste eindpunten gebruikt voor apparaat-naar-cloud-berichten][lnk-custom].</span><span class="sxs-lookup"><span data-stu-id="a2a25-142">If you want tooroute your device-to-cloud messages toocustom endpoints, see [Use message routes and custom endpoints for device-to-cloud messages][lnk-custom].</span></span>

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
