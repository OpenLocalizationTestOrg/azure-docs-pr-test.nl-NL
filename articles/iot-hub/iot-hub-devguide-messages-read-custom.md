---
title: aangepaste eindpunten van aaaUnderstand Azure IoT Hub | Microsoft Docs
description: Handleiding voor ontwikkelaars - met routering tooroute apparaat-naar-cloudberichten toocustom eindpunten regels.
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
ms.openlocfilehash: daa9cfb35d0853e316bbf469b034d4dadbd4e85d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a><span data-ttu-id="901cd-103">Berichtroutes en aangepaste eindpunten gebruikt voor apparaat-naar-cloud-berichten</span><span class="sxs-lookup"><span data-stu-id="901cd-103">Use message routes and custom endpoints for device-to-cloud messages</span></span>

<span data-ttu-id="901cd-104">IoT-Hub kunt u tooroute [apparaat-naar-cloudberichten] [ lnk-device-to-cloud] tooIoT Hub gerichte service-eindpunten op basis van eigenschappen van berichten.</span><span class="sxs-lookup"><span data-stu-id="901cd-104">IoT Hub enables you tooroute [device-to-cloud messages][lnk-device-to-cloud] tooIoT Hub service-facing endpoints based on message properties.</span></span> <span data-ttu-id="901cd-105">Routering van regels kunt u de flexibiliteit toosend Hallo moeten waar ze nodig hebben toogo zonder Hallo-berichten voor extra services tooprocess berichten of toowrite aanvullende code.</span><span class="sxs-lookup"><span data-stu-id="901cd-105">Routing rules give you hello flexibility toosend messages where they need toogo without hello need for additional services tooprocess messages or toowrite additional code.</span></span> <span data-ttu-id="901cd-106">Elke regel voor het doorsturen die u configureert heeft Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="901cd-106">Each routing rule you configure has hello following properties:</span></span>

| <span data-ttu-id="901cd-107">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="901cd-107">Property</span></span>      | <span data-ttu-id="901cd-108">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="901cd-108">Description</span></span> |
| ------------- | ----------- |
| <span data-ttu-id="901cd-109">**Naam**</span><span class="sxs-lookup"><span data-stu-id="901cd-109">**Name**</span></span>      | <span data-ttu-id="901cd-110">Hallo unieke naam zijn die Hallo regel identificeert.</span><span class="sxs-lookup"><span data-stu-id="901cd-110">hello unique name that identifies hello rule.</span></span> |
| <span data-ttu-id="901cd-111">**Bron**</span><span class="sxs-lookup"><span data-stu-id="901cd-111">**Source**</span></span>    | <span data-ttu-id="901cd-112">Hallo oorsprong van Hallo gegevens stream toobe gereageerd.</span><span class="sxs-lookup"><span data-stu-id="901cd-112">hello origin of hello data stream toobe acted upon.</span></span> <span data-ttu-id="901cd-113">Bijvoorbeeld: apparaattelemetrie.</span><span class="sxs-lookup"><span data-stu-id="901cd-113">For example, device telemetry.</span></span> |
| <span data-ttu-id="901cd-114">**Voorwaarde**</span><span class="sxs-lookup"><span data-stu-id="901cd-114">**Condition**</span></span> | <span data-ttu-id="901cd-115">Hallo query-expressie voor routering Hallo-regel die wordt uitgevoerd aan de kopteksten en de hoofdtekst Hallo-bericht en toodetermine gebruikt of u nu een overeenkomst voor het Hallo-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="901cd-115">hello query expression for hello routing rule that is run against hello message's headers and body and used toodetermine whether it is a match for hello endpoint.</span></span> <span data-ttu-id="901cd-116">Zie voor meer informatie over het maken van een voorwaarde route Hallo [referentie - querytaal voor apparaat horende en taken][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="901cd-116">For more information about constructing a route condition, see hello [Reference - query language for device twins and jobs][lnk-devguide-query-language].</span></span> |
| <span data-ttu-id="901cd-117">**Eindpunt**</span><span class="sxs-lookup"><span data-stu-id="901cd-117">**Endpoint**</span></span>  | <span data-ttu-id="901cd-118">de naam van de Hallo van Hallo eindpunt waar IoT Hub verzendt berichten die overeenkomen met Hallo voorwaarde.</span><span class="sxs-lookup"><span data-stu-id="901cd-118">hello name of hello endpoint where IoT Hub sends messages that match hello condition.</span></span> <span data-ttu-id="901cd-119">Eindpunten moet Hallo dezelfde regio bevinden als Hallo iothub, anders u mogelijk in rekening gebracht voor de regio-overschrijdende schrijft.</span><span class="sxs-lookup"><span data-stu-id="901cd-119">Endpoints should be in hello same region as hello IoT hub, otherwise you may be charged for cross-region writes.</span></span> |

<span data-ttu-id="901cd-120">Een enkel bericht mogelijk overeenkomt met de Hallo voorwaarde op meerdere regels voor het doorsturen, waarin geval IoT Hub Hallo-bericht toohello eindpunt die zijn gekoppeld aan elke overeenkomende regel biedt.</span><span class="sxs-lookup"><span data-stu-id="901cd-120">A single message may match hello condition on multiple routing rules, in which case IoT Hub delivers hello message toohello endpoint associated with each matched rule.</span></span> <span data-ttu-id="901cd-121">IoT Hub deduplicates ook automatisch levering van berichten, dus als een bericht overeenkomt met meerdere regels die allemaal Hallo hebben hetzelfde doel wordt alleen geschreven toothat bestemming eenmaal.</span><span class="sxs-lookup"><span data-stu-id="901cd-121">IoT Hub also automatically deduplicates message delivery, so if a message matches multiple rules that all have hello same destination, it is only written toothat destination once.</span></span>

<span data-ttu-id="901cd-122">Een IoT-hub is een standaard [ingebouwd eindpunt][lnk-built-in].</span><span class="sxs-lookup"><span data-stu-id="901cd-122">An IoT hub has a default [built-in endpoint][lnk-built-in].</span></span> <span data-ttu-id="901cd-123">U kunt aangepaste eindpunten tooroute berichten tooby koppelen van andere services in uw abonnement toohello hub maken.</span><span class="sxs-lookup"><span data-stu-id="901cd-123">You can create custom endpoints tooroute messages tooby linking other services in your subscription toohello hub.</span></span> <span data-ttu-id="901cd-124">IoT Hub ondersteunt momenteel Event Hubs, Service Bus-wachtrijen en Service Bus-onderwerpen als aangepaste eindpunten.</span><span class="sxs-lookup"><span data-stu-id="901cd-124">IoT Hub currently supports Event Hubs, Service Bus queues, and Service Bus topics as custom endpoints.</span></span>

> [!WARNING]
> <span data-ttu-id="901cd-125">Service Bus-wachtrijen en onderwerpen met **sessies** of **detectie van dubbele** ingeschakeld worden niet ondersteund als aangepaste eindpunten.</span><span class="sxs-lookup"><span data-stu-id="901cd-125">Service Bus queues and topics with **Sessions** or **Duplicate Detection** enabled are not supported as custom endpoints.</span></span>

<span data-ttu-id="901cd-126">Zie voor meer informatie over het maken van aangepaste eindpunten van IoT-Hub [IoT-hubeindpunten][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="901cd-126">For more information about creating custom endpoints in IoT Hub, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="901cd-127">Zie voor meer informatie over het lezen van het aangepaste eindpunten:</span><span class="sxs-lookup"><span data-stu-id="901cd-127">For more information about reading from custom endpoints, see:</span></span>

* <span data-ttu-id="901cd-128">Lezen van [Event Hubs][lnk-getstarted-eh].</span><span class="sxs-lookup"><span data-stu-id="901cd-128">Reading from [Event Hubs][lnk-getstarted-eh].</span></span>
* <span data-ttu-id="901cd-129">Lezen van [Service Bus-wachtrijen][lnk-getstarted-queue].</span><span class="sxs-lookup"><span data-stu-id="901cd-129">Reading from [Service Bus queues][lnk-getstarted-queue].</span></span>
* <span data-ttu-id="901cd-130">Lezen van [Service Bus-onderwerpen][lnk-getstarted-topic].</span><span class="sxs-lookup"><span data-stu-id="901cd-130">Reading from [Service Bus topics][lnk-getstarted-topic].</span></span>

### <a name="next-steps"></a><span data-ttu-id="901cd-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="901cd-131">Next steps</span></span>

<span data-ttu-id="901cd-132">Zie voor meer informatie over IoT-hubeindpunten [IoT-hubeindpunten][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="901cd-132">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="901cd-133">Voor meer informatie over het Hallo-querytaal u regels voor het doorsturen van toodefine gebruiken, Zie [querytaal IoT Hub voor apparaat horende, taken en berichtroutering][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="901cd-133">For more information about hello query language you use toodefine routing rules, see [IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query-language].</span></span>

<span data-ttu-id="901cd-134">Hallo [proces IoT Hub apparaat-naar-cloud-berichten met behulp van routes] [ lnk-d2c-tutorial] zelfstudie laat zien u hoe toouse routering regels en aangepaste eindpunten.</span><span class="sxs-lookup"><span data-stu-id="901cd-134">hello [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial shows you how toouse routing rules and custom endpoints.</span></span>

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
