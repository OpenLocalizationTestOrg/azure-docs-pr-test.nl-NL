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
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a>Berichtroutes en aangepaste eindpunten gebruikt voor apparaat-naar-cloud-berichten

IoT-Hub kunt u tooroute [apparaat-naar-cloudberichten] [ lnk-device-to-cloud] tooIoT Hub gerichte service-eindpunten op basis van eigenschappen van berichten. Routering van regels kunt u de flexibiliteit toosend Hallo moeten waar ze nodig hebben toogo zonder Hallo-berichten voor extra services tooprocess berichten of toowrite aanvullende code. Elke regel voor het doorsturen die u configureert heeft Hallo volgende eigenschappen:

| Eigenschap      | Beschrijving |
| ------------- | ----------- |
| **Naam**      | Hallo unieke naam zijn die Hallo regel identificeert. |
| **Bron**    | Hallo oorsprong van Hallo gegevens stream toobe gereageerd. Bijvoorbeeld: apparaattelemetrie. |
| **Voorwaarde** | Hallo query-expressie voor routering Hallo-regel die wordt uitgevoerd aan de kopteksten en de hoofdtekst Hallo-bericht en toodetermine gebruikt of u nu een overeenkomst voor het Hallo-eindpunt. Zie voor meer informatie over het maken van een voorwaarde route Hallo [referentie - querytaal voor apparaat horende en taken][lnk-devguide-query-language]. |
| **Eindpunt**  | de naam van de Hallo van Hallo eindpunt waar IoT Hub verzendt berichten die overeenkomen met Hallo voorwaarde. Eindpunten moet Hallo dezelfde regio bevinden als Hallo iothub, anders u mogelijk in rekening gebracht voor de regio-overschrijdende schrijft. |

Een enkel bericht mogelijk overeenkomt met de Hallo voorwaarde op meerdere regels voor het doorsturen, waarin geval IoT Hub Hallo-bericht toohello eindpunt die zijn gekoppeld aan elke overeenkomende regel biedt. IoT Hub deduplicates ook automatisch levering van berichten, dus als een bericht overeenkomt met meerdere regels die allemaal Hallo hebben hetzelfde doel wordt alleen geschreven toothat bestemming eenmaal.

Een IoT-hub is een standaard [ingebouwd eindpunt][lnk-built-in]. U kunt aangepaste eindpunten tooroute berichten tooby koppelen van andere services in uw abonnement toohello hub maken. IoT Hub ondersteunt momenteel Event Hubs, Service Bus-wachtrijen en Service Bus-onderwerpen als aangepaste eindpunten.

> [!WARNING]
> Service Bus-wachtrijen en onderwerpen met **sessies** of **detectie van dubbele** ingeschakeld worden niet ondersteund als aangepaste eindpunten.

Zie voor meer informatie over het maken van aangepaste eindpunten van IoT-Hub [IoT-hubeindpunten][lnk-devguide-endpoints].

Zie voor meer informatie over het lezen van het aangepaste eindpunten:

* Lezen van [Event Hubs][lnk-getstarted-eh].
* Lezen van [Service Bus-wachtrijen][lnk-getstarted-queue].
* Lezen van [Service Bus-onderwerpen][lnk-getstarted-topic].

### <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over IoT-hubeindpunten [IoT-hubeindpunten][lnk-devguide-endpoints].

Voor meer informatie over het Hallo-querytaal u regels voor het doorsturen van toodefine gebruiken, Zie [querytaal IoT Hub voor apparaat horende, taken en berichtroutering][lnk-devguide-query-language].

Hallo [proces IoT Hub apparaat-naar-cloud-berichten met behulp van routes] [ lnk-d2c-tutorial] zelfstudie laat zien u hoe toouse routering regels en aangepaste eindpunten.

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
