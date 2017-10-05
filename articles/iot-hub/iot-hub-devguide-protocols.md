---
title: Azure IoT Hub communicatieprotocollen en poorten | Microsoft Docs
description: Handleiding voor ontwikkelaars - beschrijft de ondersteunde communicatieprotocollen voor apparaat-naar-cloud-en cloud-naar-apparaat en de poortnummers die geopend zijn moeten.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3fc5f1a3-3711-4611-9897-d4db079b4250
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 98004a48734e33f85eebf8f6213d9f0751dea843
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# Verwijzen naar - een communicatieprotocol kiezen

IoT Hub-apparaten kunt [MQTT][lnk-mqtt], MQTT via WebSockets, [AMQP][lnk-amqp], AMQP over WebSockets en HTTP-protocollen voor apparaat-zijde communicatie. Zie voor meer informatie over hoe deze protocollen specifieke IoT-Hub-functies ondersteunen [apparaat-naar-cloud communicatie richtlijnen] [ lnk-d2c-guidance] en [Cloud-naar-apparaat communicatie richtlijnen] [lnk-c2d-guidance].

De volgende tabel bevat de op hoog niveau aanbevelingen voor uw keuze van het protocol:

| Protocol | Wanneer u dit protocol moet kiezen |
| --- | --- |
| MQTT <br> MQTT via WebSocket |Gebruik op alle apparaten die niet hoeven via dezelfde TLS-verbinding verbinding te maken van meerdere apparaten (elk met zijn eigen referenties per apparaat). |
| AMQP <br> AMQP via WebSocket |Op veld en cloud-gateways gebruiken om te profiteren van de verbinding multiplex verschillende apparaten. |
| HTTP |Gebruik dit voor apparaten die niet kan, andere protocollen ondersteunen. |

Houd rekening met de volgende punten wanneer u ervoor uw protocol voor het apparaat aan clientzijde communicatie kiest:

* **Cloud-naar-apparaat patroon**. HTTP beschikt niet over een efficiënte manier voor het implementeren van server-push. Als zodanig wanneer u HTTP gebruikt, pollen apparaten IoT Hub voor cloud-naar-apparaat-berichten. Deze aanpak is inefficiënt voor het apparaat en de IoT-Hub. Onder de huidige richtlijnen voor HTTP, moet elk apparaat voor berichten pollen, elke 25 minuten of langer. Aan de andere kant MQTT en AMQP ondersteunen server push tijdens het ontvangen van berichten van de cloud-naar-apparaat. Ze inschakelen direct pushes van berichten uit IoT Hub naar het apparaat. Als levering latentie is een probleem, zijn MQTT of AMQP de aanbevolen protocollen gebruiken. Voor zelden verbonden apparaten, wordt HTTP ook werkt.
* **Veld gateways**. Wanneer u MQTT en HTTP gebruikt, u meerdere apparaten (elk met zijn eigen referenties per apparaat) kan geen verbinding kunt maken met behulp van dezelfde TLS-verbinding. Dus voor [veld gatewayscenario's][lnk-azure-gateway-guidance], deze protocollen zijn suboptimale omdat zij één TLS-verbinding tussen de veldgateway en IoT Hub voor elk apparaat is verbonden met de veldgateway is vereist.
* **Resource apparaten geringe**. De protocollen MQTT en HTTP-bibliotheken hebben een kleiner oppervlak dan het AMQP-bibliotheken. Als zodanig als het apparaat resources (voor bijvoorbeeld minder dan 1 MB RAM) beperkt heeft, zijn deze protocollen de enige protocol-implementatie.
* **{De passage netwerk**. Het standaard AMQP-protocol maakt gebruik van poort 5671, terwijl MQTT luistert op poort 8883, die problemen kan veroorzaken in netwerken die niet-HTTP-protocollen worden gesloten. MQTT via WebSockets AMQP over WebSockets en HTTP zijn beschikbaar voor gebruik in dit scenario.
* **Pakketgrootte**. MQTT en AMQP zijn binaire protocollen, waardoor het meer compacte nettoladingen dan HTTP.

> [!WARNING]
> Wanneer u HTTP gebruikt, moet elk apparaat voor cloud-naar-apparaat-berichten pollen elke 25 minuten of langer. Tijdens de ontwikkeling is het echter aanvaardbaar is voor het pollen vaker dan elke 25 minuten.

## Poortnummers

Apparaten kunnen communiceren met IoT Hub in Azure met behulp van verschillende protocollen. Normaal gesproken wordt de keuze van het protocol bepaald door de specifieke vereisten van de oplossing. De volgende tabel bevat de uitgaande poorten die moeten zijn geopend voor een apparaat om te kunnen gebruiken van een specifiek protocol:

| Protocol | Poort |
| --- | --- |
| MQTT |8883 |
| MQTT via WebSockets |443 |
| AMQP |5671 |
| AMQP via WebSockets |443 |
| HTTP |443 |

Nadat u een IoT-hub hebt gemaakt in een Azure-regio, houdt de IoT-hub hetzelfde IP-adres voor de levensduur van iothub. Echter als u wilt behouden quality of service,-als Microsoft de IoT-hub naar een andere schaaleenheid verplaatst vervolgens krijgt het een nieuw IP-adres.


## Volgende stappen

Zie voor meer informatie over hoe IoT Hub het MQTT-protocol implementeert, [communiceren met uw iothub met het protocol MQTT][lnk-mqtt-support].

[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-mqtt-support]: iot-hub-mqtt-support.md
[lnk-amqp]: http://docs.oasis-open.org/amqp/core/v1.0/os/amqp-core-complete-v1.0-os.pdf
[lnk-mqtt]: http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/mqtt-v3.1.1.pdf
[lnk-azure-gateway-guidance]: iot-hub-devguide-endpoints.md#field-gateways
