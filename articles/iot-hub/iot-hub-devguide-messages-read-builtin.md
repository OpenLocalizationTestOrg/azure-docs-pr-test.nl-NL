---
title: Inzicht in de Azure IoT Hub ingebouwd eindpunt | Microsoft Docs
description: Handleiding voor ontwikkelaars - beschrijft het gebruik van de ingebouwde Event Hub-compatibele eindpunt toread apparaat-naar-cloud-berichten.
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
ms.openlocfilehash: fcc3743028e369fdc42b71887d49fb41fba2c0dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="read-device-to-cloud-messages-from-the-built-in-endpoint"></a><span data-ttu-id="e9770-103">Apparaat-naar-cloud-berichten lezen van het ingebouwde eindpunt</span><span class="sxs-lookup"><span data-stu-id="e9770-103">Read device-to-cloud messages from the built-in endpoint</span></span>

<span data-ttu-id="e9770-104">Standaard berichten worden doorgestuurd naar het ingebouwde gerichte service-eindpunt (**berichten/gebeurtenissen**), die compatibel is met [Event Hubs][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="e9770-104">By default, messages are routed to the built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="e9770-105">Dit eindpunt is momenteel alleen zichtbare met behulp van de [AMQP] [ lnk-amqp] -protocol op poort 5671.</span><span class="sxs-lookup"><span data-stu-id="e9770-105">This endpoint is currently only exposed using the [AMQP][lnk-amqp] protocol on port 5671.</span></span> <span data-ttu-id="e9770-106">Een IoT-hub toont de volgende eigenschappen om te bepalen van de ingebouwde Event Hub-compatibele messaging eindpunt **berichten/gebeurtenissen**.</span><span class="sxs-lookup"><span data-stu-id="e9770-106">An IoT hub exposes the following properties to enable you to control the built-in Event Hub-compatible messaging endpoint **messages/events**.</span></span>

| <span data-ttu-id="e9770-107">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="e9770-107">Property</span></span>            | <span data-ttu-id="e9770-108">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e9770-108">Description</span></span> |
| ------------------- | ----------- |
| <span data-ttu-id="e9770-109">**Aantal partities**</span><span class="sxs-lookup"><span data-stu-id="e9770-109">**Partition count**</span></span> | <span data-ttu-id="e9770-110">Stel deze eigenschap bij het maken van het aantal definiëren [partities] [ lnk-event-hub-partitions] voor opname van apparaat-naar-cloud-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="e9770-110">Set this property at creation to define the number of [partitions][lnk-event-hub-partitions] for device-to-cloud event ingestion.</span></span> |
| <span data-ttu-id="e9770-111">**Bewaartijd**</span><span class="sxs-lookup"><span data-stu-id="e9770-111">**Retention time**</span></span>  | <span data-ttu-id="e9770-112">Deze eigenschap specificeert hoe lang in dagen dat berichten door de IoT Hub worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="e9770-112">This property specifies how long in days messages are retained by IoT Hub.</span></span> <span data-ttu-id="e9770-113">De standaardwaarde is één dag, maar deze kan worden verhoogd tot zeven dagen.</span><span class="sxs-lookup"><span data-stu-id="e9770-113">The default is one day, but it can be increased to seven days.</span></span> |

<span data-ttu-id="e9770-114">IoT-Hub kunt u beheren consumer-groepen op de ingebouwde apparaat-naar-cloud eindpunt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="e9770-114">IoT Hub also enables you to manage consumer groups on the built-in device-to-cloud receive endpoint.</span></span>

<span data-ttu-id="e9770-115">Standaard worden alle berichten die niet expliciet overeen met een regel voor het doorsturen van een bericht geschreven naar het eindpunt van de ingebouwde.</span><span class="sxs-lookup"><span data-stu-id="e9770-115">By default, all messages that do not explicitly match a message routing rule are written to the built-in endpoint.</span></span> <span data-ttu-id="e9770-116">Als u deze route voor terugval uitschakelt, worden berichten die niet expliciet overeen met alle regels voor het doorsturen van bericht verwijderd.</span><span class="sxs-lookup"><span data-stu-id="e9770-116">If you disable this fallback route, messages that do not explicitly match any message routing rules are dropped.</span></span>

<span data-ttu-id="e9770-117">U kunt ofwel de bewaartijd wijzigen programmatisch via de [resourceprovider IoT Hub REST-API's][lnk-resource-provider-apis], of met behulp van de [Azure-portal][lnk-management-portal].</span><span class="sxs-lookup"><span data-stu-id="e9770-117">You can modify the retention time, either programmatically through the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis], or by using the [Azure portal][lnk-management-portal].</span></span>

<span data-ttu-id="e9770-118">IoT-Hub toont de **berichten/gebeurtenissen** ingebouwd eindpunt voor uw back-end-services om te lezen van de apparaat-naar-cloud-berichten dat is ontvangen door de hub.</span><span class="sxs-lookup"><span data-stu-id="e9770-118">IoT Hub exposes the **messages/events** built-in endpoint for your back-end services to read the device-to-cloud messages received by your hub.</span></span> <span data-ttu-id="e9770-119">Dit eindpunt is Event Hub-compatibele, waarmee u een van de mechanismen gebruiken de Event Hubs-service ondersteunt voor het lezen van berichten.</span><span class="sxs-lookup"><span data-stu-id="e9770-119">This endpoint is Event Hub-compatible, which enables you to use any of the mechanisms the Event Hubs service supports for reading messages.</span></span>

## <a name="read-from-the-built-in-endpoint"></a><span data-ttu-id="e9770-120">Lezen van het ingebouwde eindpunt</span><span class="sxs-lookup"><span data-stu-id="e9770-120">Read from the built-in endpoint</span></span>

<span data-ttu-id="e9770-121">Wanneer u gebruikt de [Azure Service Bus-SDK voor .NET] [ lnk-servicebus-sdk] of de [Event Hubs - Gebeurtenisprocessorhost][lnk-eventprocessorhost], kunt u eventuele verbindingstekenreeksen IoT Hub met de juiste machtigingen.</span><span class="sxs-lookup"><span data-stu-id="e9770-121">When you use the [Azure Service Bus SDK for .NET][lnk-servicebus-sdk] or the [Event Hubs - Event Processor Host][lnk-eventprocessorhost], you can use any IoT Hub connection strings with the correct permissions.</span></span> <span data-ttu-id="e9770-122">Gebruik vervolgens **berichten/gebeurtenissen** als de naam van de Event Hub.</span><span class="sxs-lookup"><span data-stu-id="e9770-122">Then use **messages/events** as the Event Hub name.</span></span>

<span data-ttu-id="e9770-123">Wanneer u SDK's (of product integraties) gebruikt die zich niet bewust zijn van IoT Hub, moet u een Event Hub-compatibele eindpunt en een Event Hub-compatibele naam ophalen uit de IoT Hub-instellingen in de [Azure-portal][lnk-management-portal]:</span><span class="sxs-lookup"><span data-stu-id="e9770-123">When you use SDKs (or product integrations) that are unaware of IoT Hub, you must retrieve an Event Hub-compatible endpoint and Event Hub-compatible name from the IoT Hub settings in the [Azure portal][lnk-management-portal]:</span></span>

1. <span data-ttu-id="e9770-124">Klik in de blade IoT hub **eindpunten**.</span><span class="sxs-lookup"><span data-stu-id="e9770-124">In the IoT hub blade, click **Endpoints**.</span></span>
1. <span data-ttu-id="e9770-125">In de **ingebouwde eindpunten** sectie, klikt u op **gebeurtenissen**.</span><span class="sxs-lookup"><span data-stu-id="e9770-125">In the **Built-in endpoints** section, click **Events**.</span></span> <span data-ttu-id="e9770-126">De blade bevat de volgende waarden: **Event Hub-compatibele eindpunt**, **Event Hub-compatibele naam**, **partities**, **bewaartijd**, en **consumergroepen**.</span><span class="sxs-lookup"><span data-stu-id="e9770-126">The blade contains the following values: **Event Hub-compatible endpoint**, **Event Hub-compatible name**, **Partitions**, **Retention time**, and **Consumer groups**.</span></span>

    ![Apparaat-naar-cloud-instellingen][img-eventhubcompatible]

<span data-ttu-id="e9770-128">De naam voor het eindpunt van IoT Hub, die is vereist dat de IoT Hub SDK **berichten/gebeurtenissen** zoals weergegeven in de **eindpunten** blade.</span><span class="sxs-lookup"><span data-stu-id="e9770-128">The IoT Hub SDK requires the IoT Hub endpoint name, which is **messages/events** as shown in the **Endpoints** blade.</span></span>

<span data-ttu-id="e9770-129">Als de SDK die u moet een **hostnaam** of **Namespace** waarde, verwijdert u het schema van de **Event Hub-compatibele eindpunt**.</span><span class="sxs-lookup"><span data-stu-id="e9770-129">If the SDK you are using requires a **Hostname** or **Namespace** value, remove the scheme from the **Event Hub-compatible endpoint**.</span></span> <span data-ttu-id="e9770-130">Bijvoorbeeld, als uw Event Hub-compatibele eindpunt **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, wordt de **hostnaam** zou **iothub-ns-myiothub-1234.servicebus.windows.net**, en de **Namespace** zou **iothub-ns-myiothub-1234**.</span><span class="sxs-lookup"><span data-stu-id="e9770-130">For example, if your Event Hub-compatible endpoint is **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, the **Hostname** would be **iothub-ns-myiothub-1234.servicebus.windows.net**, and the **Namespace** would be **iothub-ns-myiothub-1234**.</span></span>

<span data-ttu-id="e9770-131">U kunt een beleid voor gedeelde toegang met de **ServiceConnect** machtigingen verbinding maken met de opgegeven Event Hub.</span><span class="sxs-lookup"><span data-stu-id="e9770-131">You can then use any shared access policy that has the **ServiceConnect** permissions to connect to the specified Event Hub.</span></span>

<span data-ttu-id="e9770-132">Als u een Event Hub-verbindingsreeks bouwen wilt met behulp van de vorige gegevens, gebruikt u het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="e9770-132">If you need to build an Event Hub connection string by using the previous information, use the following pattern:</span></span>

`Endpoint={Event Hub-compatible endpoint};SharedAccessKeyName={iot hub policy name};SharedAccessKey={iot hub policy key}`

<span data-ttu-id="e9770-133">De SDK's en integraties gebruikt die u kunt gebruiken met Event Hub-compatibele eindpunten die IoT-Hub toont bevat de items in de volgende lijst:</span><span class="sxs-lookup"><span data-stu-id="e9770-133">The SDKs and integrations that you can use with Event Hub-compatible endpoints that IoT Hub exposes includes the items in the following list:</span></span>

* <span data-ttu-id="e9770-134">[Java Event Hubs-client](https://github.com/hdinsight/eventhubs-client).</span><span class="sxs-lookup"><span data-stu-id="e9770-134">[Java Event Hubs client](https://github.com/hdinsight/eventhubs-client).</span></span>
* <span data-ttu-id="e9770-135">[Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="e9770-135">[Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span> <span data-ttu-id="e9770-136">U vindt de [spout bron](https://github.com/apache/storm/tree/master/external/storm-eventhubs) op GitHub.</span><span class="sxs-lookup"><span data-stu-id="e9770-136">You can view the [spout source](https://github.com/apache/storm/tree/master/external/storm-eventhubs) on GitHub.</span></span>
* <span data-ttu-id="e9770-137">[Apache Spark-integratie](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span><span class="sxs-lookup"><span data-stu-id="e9770-137">[Apache Spark integration](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9770-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e9770-138">Next steps</span></span>

<span data-ttu-id="e9770-139">Zie voor meer informatie over IoT-hubeindpunten [IoT-hubeindpunten][lnk-endpoints].</span><span class="sxs-lookup"><span data-stu-id="e9770-139">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-endpoints].</span></span>

<span data-ttu-id="e9770-140">De [aan de slag] [ lnk-get-started] zelfstudies ziet u hoe u apparaat-naar-cloud-berichten verzenden van de gesimuleerde apparaten en de berichten lezen van het ingebouwde eindpunt.</span><span class="sxs-lookup"><span data-stu-id="e9770-140">The [Get Started][lnk-get-started] tutorials show you how to send device-to-cloud messages from simulated devices and read the messages from the built-in endpoint.</span></span> <span data-ttu-id="e9770-141">Zie voor meer details over de [proces IoT Hub apparaat-naar-cloud-berichten met behulp van routes] [ lnk-d2c-tutorial] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="e9770-141">For more detail, see the [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

<span data-ttu-id="e9770-142">Als u wilt voor het routeren van uw apparaat-naar-cloud-berichten met aangepaste eindpunten, Zie [berichtroutes en aangepaste eindpunten gebruikt voor apparaat-naar-cloud-berichten][lnk-custom].</span><span class="sxs-lookup"><span data-stu-id="e9770-142">If you want to route your device-to-cloud messages to custom endpoints, see [Use message routes and custom endpoints for device-to-cloud messages][lnk-custom].</span></span>

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
