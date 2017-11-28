---
title: protocollen en poorten voor communicatie met IoT Hub aaaAzure | Microsoft Docs
description: Handleiding voor ontwikkelaars - beschrijft communicatieprotocollen Hallo ondersteund voor apparaat-naar-cloud- en cloud-naar-apparaat communicatie en Hallo poortnummers die geopend zijn moeten.
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
ms.openlocfilehash: 31cb948f1d30edd87edb13ad0dd859c02bcc3239
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# Verwijzen naar - een communicatieprotocol kiezen

IoT-Hub kunt apparaten toouse [MQTT][lnk-mqtt], MQTT via WebSockets, [AMQP][lnk-amqp], AMQP over WebSockets en HTTP-protocollen voor apparaat-zijde communicatie. Zie voor meer informatie over hoe deze protocollen specifieke IoT-Hub-functies ondersteunen [apparaat-naar-cloud communicatie richtlijnen] [ lnk-d2c-guidance] en [Cloud-naar-apparaat communicatie richtlijnen] [lnk-c2d-guidance].

Hallo bevat volgende tabel Hallo op hoog niveau aanbevelingen voor uw keuze van protocol:

| Protocol | Wanneer u dit protocol moet kiezen |
| --- | --- |
| MQTT <br> MQTT via WebSocket |Gebruiken om meerdere apparaten (elk met zijn eigen referenties per apparaat) op alle apparaten die niet te worden tooconnect hoeven over Hallo dezelfde TLS-verbinding. |
| AMQP <br> AMQP via WebSocket |Op het veld en cloud gateways tootake profiteren van verschillende apparaten multiplex verbinding gebruiken. |
| HTTP |Gebruik dit voor apparaten die niet kan, andere protocollen ondersteunen. |

Overweeg de volgende punten wanneer u ervoor uw protocol voor het apparaat aan clientzijde communicatie kiest Hallo:

* **Cloud-naar-apparaat patroon**. HTTP beschikt niet over een efficiënte manier tooimplement server push. Als zodanig wanneer u HTTP gebruikt, pollen apparaten IoT Hub voor cloud-naar-apparaat-berichten. Deze aanpak is inefficiënt voor zowel Hallo-apparaat en IoT Hub. Onder de huidige richtlijnen voor HTTP, moet elk apparaat voor berichten pollen, elke 25 minuten of langer. Op Hallo daarentegen, MQTT en AMQP server push ondersteunen bij het ontvangen van berichten van de cloud-naar-apparaat. Ze inschakelen direct pushes van berichten uit IoT Hub toohello apparaat. Als levering latentie belangrijk is, zijn protocollen MQTT of AMQP Hallo best protocollen toouse. Voor zelden verbonden apparaten, wordt HTTP ook werkt.
* **Veld gateways**. Wanneer u MQTT en HTTP gebruikt, u meerdere apparaten (elk met zijn eigen referenties per apparaat) kan geen verbinding kunt maken met behulp van Hallo dezelfde TLS-verbinding. Dus voor [veld gatewayscenario's][lnk-azure-gateway-guidance], deze protocollen zijn suboptimale omdat ze een TLS-verbinding tussen Hallo veldgateway en IoT Hub voor elk apparaat verbonden toohello veldgateway vereisen.
* **Resource apparaten geringe**. Hallo MQTT en HTTP-bibliotheken hebt een kleiner oppervlak dan Hallo AMQP-bibliotheken. Als zodanig, als hello apparaat beperkte bronnen (bijvoorbeeld minder dan 1 MB RAM), deze protocollen mogelijk Hallo alleen protocolimplementatie beschikbaar.
* **{De passage netwerk**. Hallo AMQP-protocol maakt gebruik van poort 5671, terwijl MQTT luistert op poort 8883, die problemen kan veroorzaken in netwerken die gesloten toonon-HTTP-protocollen zijn. MQTT via WebSockets AMQP over WebSockets en HTTP zijn beschikbaar toobe in dit scenario gebruikt.
* **Pakketgrootte**. MQTT en AMQP zijn binaire protocollen, waardoor het meer compacte nettoladingen dan HTTP.

> [!WARNING]
> Wanneer u HTTP gebruikt, moet elk apparaat voor cloud-naar-apparaat-berichten pollen elke 25 minuten of langer. Tijdens de ontwikkeling is het echter acceptabele toopoll vaker dan elke 25 minuten.

## Poortnummers

Apparaten kunnen communiceren met IoT Hub in Azure met behulp van verschillende protocollen. Normaal gesproken wordt Hallo gekozen protocol aangedreven door specifieke vereisten van de oplossing Hallo Hallo. Hallo bevat volgende tabel Hallo uitgaande poorten die geopend voor een apparaat toobe kunnen toouse een specifiek protocol zijn moeten:

| Protocol | Poort |
| --- | --- |
| MQTT |8883 |
| MQTT via WebSockets |443 |
| AMQP |5671 |
| AMQP via WebSockets |443 |
| HTTP |443 |

Nadat u een IoT-hub hebt gemaakt in een Azure-regio, hello hello IoT hub houdt hetzelfde IP-adres voor Hallo levensduur van iothub. Quality of service, als Microsoft hello IoT hub tooa verschillende schaaleenheid wordt verplaatst-toomaintain is echter een nieuwe IP-adres toegewezen.


## Volgende stappen

toolearn meer informatie over hoe IoT Hub implementeert Hallo MQTT protocol, Zie [communiceren met uw iothub met Hallo MQTT protocol][lnk-mqtt-support].

[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-mqtt-support]: iot-hub-mqtt-support.md
[lnk-amqp]: http://docs.oasis-open.org/amqp/core/v1.0/os/amqp-core-complete-v1.0-os.pdf
[lnk-mqtt]: http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/mqtt-v3.1.1.pdf
[lnk-azure-gateway-guidance]: iot-hub-devguide-endpoints.md#field-gateways
