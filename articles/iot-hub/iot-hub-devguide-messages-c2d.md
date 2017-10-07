---
title: Azure IoT Hub cloud-naar-apparaat aaaUnderstand messaging | Microsoft Docs
description: Handleiding voor ontwikkelaars - hoe toouse cloud-naar-apparaat met IoT Hub berichten. Bevat informatie over de levenscyclus van de Hallo-bericht en configuratieopties.
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
ms.openlocfilehash: 5c747b50163873d823556a8baa769c4b8f7f8c44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-from-iot-hub"></a>Cloud-naar-apparaat-berichten uit IoT Hub verzenden

toosend eenzijdige meldingen toohello apparaat app van uw back-end oplossing, verzonden berichten van cloud naar apparaten van uw IoT hub tooyour apparaat. Zie voor een beschrijving van de andere opties cloud naar apparaten die worden ondersteund door de IoT Hub, [Cloud-naar-apparaat communicatie richtlijnen][lnk-c2d-guidance].

Verzenden van berichten van de cloud-naar-apparaat via een gerichte service-eindpunt (**berichten/devicebound**). Een apparaat ontvangt vervolgens Hallo-berichten via een eindpunt apparaatspecifieke (**/devices/ {deviceId} / berichten/devicebound**).

Elk bericht cloud-naar-apparaat is gericht op één apparaat door de instelling Hallo **naar** eigenschap te**/devices/ {deviceId} / berichten/devicebound**.

Elke apparaatwachtrij bevat maximaal 50 cloud-naar-apparaat-berichten. Probeert toosend meer berichten toohello resulteert hetzelfde apparaat in een fout.

## <a name="hello-cloud-to-device-message-lifecycle"></a>Hallo cloud-naar-apparaat bericht levenscyclus

tooguarantee op in de minste eenmaal berichtbezorging, IoT-Hub persistente cloud-naar-apparaat-berichten in per apparaat wachtrijen. Apparaten moeten expliciet bevestigen *voltooiing* voor IoT Hub tooremove Hallo uit wachtrij. Deze aanpak wordt gegarandeerd dat tolerantie tegen connectiviteit en tegen fouten.

Hallo volgende diagram toont Hallo lifecycle status grafiek voor een cloud-naar-apparaat-bericht in IoT-Hub.

![De levenscyclus van de cloud-naar-apparaat-bericht][img-lifecycle]

Hallo-berichtstatus wanneer Hallo service IoT Hub verzendt een bericht tooa apparaat, het Hallo-service te ingesteld**in wachtrij gezet**. Wanneer een apparaat te wil*ontvangen* een bericht voor de IoT Hub *vergrendelingen* Hallo-bericht (door Hallo staat te stellen**onzichtbaar**), waarmee andere threads op Hallo apparaat toostart ontvangen van andere berichten. Wanneer een apparaat-thread is voltooid Hallo verwerking van een bericht, meldt deze IoT Hub door *voltooien* Hallo-bericht. IoT Hub wordt ingesteld Hallo status te**voltooid**.

Een apparaat kunt ook:

* *Afwijzen* Hallo-bericht, waardoor tooset IoT Hub het toohello **Deadlettered** status. Apparaten die verbinding via Hallo MQTT protocol maken afwijzen niet cloud-naar-apparaat-berichten.
* *Afbreken* Hallo-bericht, waardoor IoT Hub het Hallo-bericht tooput terug in de wachtrij op Hallo en met Hallo staat te stellen**in wachtrij gezet**.

Een thread kan tooprocess een bericht zonder dit IoT-Hub te mislukken. In dit geval automatisch overgang van Hallo-berichten **onzichtbaar** status back toohello **in wachtrij gezet** status na een *zichtbaarheid (of vergrendelen) time-out*. Hallo-standaardwaarde van deze time-out is 1 minuut.

Een bericht kan worden overgedragen tussen Hallo **in wachtrij gezet** en **onzichtbaar** statussen, ten hoogste aantal keren opgegeven in Hallo Hallo **max. aantal levering** eigenschap in IoT Hub. Na dit aantal transities IoT Hub stelt Hallo status van het Hallo-bericht te**Deadlettered**. Op deze manier IoT Hub stelt Hallo status van een bericht te**Deadlettered** na de verlooptijd (Zie [tijd toolive][lnk-ttl]).

Hallo [hoe toosend cloud-naar-apparaat met IoT Hub berichten] [ lnk-c2d-tutorial] ziet u hoe toosend cloud-naar-apparaat-berichten van Hallo cloud en deze op een apparaat te ontvangen.

Een apparaat is normaal gesproken een cloud-naar-apparaat-bericht voltooid wanneer Hallo verlies van het Hallo-bericht heeft geen invloed op het Hallo-toepassingslogica. Bijvoorbeeld wanneer Hallo apparaat heeft gehandhaafd berichtinhoud lokaal hello of een bewerking met succes is uitgevoerd. Hallo-bericht kan ook uitvoeren voor tijdelijke informatie waarvan verlies Hallo-functionaliteit van de toepassing hello niet gevolgen zou hebben. Soms voor langlopende taken worden uitgevoerd, kunt u voltooien Hallo-bericht van cloud-naar-apparaat behouden blijven na de Hallo taakbeschrijving van de in de lokale opslag. U kunt een melding Hallo back-end oplossing met een of meer apparaat-naar-cloud-berichten in verschillende stadia van de voortgang van Hallo taak.

## <a name="message-expiration-time-toolive"></a>Verloopdatum voor het bericht (tijd toolive)

Elk bericht dat cloud-naar-apparaat heeft een verlooptijd. Deze tijd is ingesteld door het Hallo-service (in Hallo **ExpiryTimeUtc** eigenschap), of door de IoT Hub met Hallo standaard *tijd toolive* opgegeven als een eigenschap IoT Hub. Zie [configuratieopties voor Cloud-naar-apparaat][lnk-c2d-configuration].

Een algemene manier tootake voordeel van bericht verlopen en voorkomen toodisconnected apparaten verzenden van berichten, tooset toolive korte tijd-waarden. Deze aanpak realiseert Hallo hetzelfde resultaat als het Hallo-Apparaatstatus verbinding onderhouden tijdens efficiënter wordt. Wanneer u een bericht bevestigingen aanvraagt, IoT-Hub ontvangt u een melding welke apparaten kunnen tooreceive berichten zijn en welke apparaten zijn niet online of zijn mislukt.

## <a name="message-feedback"></a>Bericht feedback

Wanneer u een cloud naar apparaat verzenden kunt Hallo serviceaanvraag Hallo levering van per bericht feedback met betrekking tot de eindstatus Hallo van dat bericht.

| ACK-eigenschap | Gedrag |
| ------------ | -------- |
| **positief** | IoT Hub een feedbackbericht genereert als en alleen als cloud-naar-apparaat het Hallo-bericht bereikt Hallo **voltooid** status. |
| **negatieve** | IoT Hub een feedbackbericht genereert als, cloud-naar-apparaat het Hallo-bericht bereikt Hallo **Deadlettered** status. |
| **volledige**     | IoT Hub genereert een feedbackbericht in beide gevallen. |

Als **Ack** is **volledige**, en u niet een feedbackbericht ontvangt, betekent dit dat feedback het Hallo-bericht is verlopen. Hallo-service kan niet weet wat is er gebeurd toohello oorspronkelijke bericht. In de praktijk kan een service Zorg ervoor dat deze Hallo feedback verwerken kan voordat deze verloopt. de maximale verlooptijdstip Hallo is twee dagen waarmee voldoende tijd tooget Hallo service nogmaals uit te voeren als er een fout optreedt.

Zoals uitgelegd in [eindpunten][lnk-endpoints], IoT-Hub levert feedback via een gerichte service-eindpunt (**/messages/servicebound/feedback**) als berichten. Hallo semantiek voor het ontvangen van feedback zijn dezelfde als voor cloud-naar-apparaatberichten Hallo en hebben dezelfde Hallo [bericht lifecycle][lnk-lifecycle]. Indien mogelijk bericht feedback in batch wordt verwerkt in een enkel bericht Hello volgende indeling:

| Eigenschap     | Beschrijving |
| ------------ | ----------- |
| EnqueuedTime | De tijdstempel die aangeeft wanneer het Hallo-bericht is gemaakt. |
| Gebruikers-id       | `{iot hub name}` |
| ContentType  | `application/vnd.microsoft.iothub.feedback.json` |

Hallo-instantie is een JSON-geserialiseerd matrix van records, elk met Hallo volgende eigenschappen:

| Eigenschap           | Beschrijving |
| ------------------ | ----------- |
| EnqueuedTimeUtc    | De tijdstempel die aangeeft wanneer Hallo resultaat van het Hallo-bericht is er gebeurd. Bijvoorbeeld, Hallo apparaat is voltooid of het Hallo-bericht is verlopen. |
| OriginalMessageId  | **MessageId** van Hallo cloud-naar-apparaat bericht toowhich deze informatie feedback betrekking heeft. |
| statusCode         | Een vereiste tekenreeks. In de feedbackberichten die gegenereerd worden door de IoT Hub gebruikt. <br/> 'Geslaagd' <br/> 'Verlopen' <br/> 'DeliveryCountExceeded' <br/> 'Geweigerd' <br/> 'Opgeschoond' |
| Beschrijving        | Waarden voor de tekenreeks **StatusCode**. |
| Apparaat-id           | **DeviceId** van het doelapparaat Hallo van Hallo cloud-naar-apparaat bericht toowhich deze stukje feedback betrekking heeft. |
| DeviceGenerationId | **DeviceGenerationId** van het doelapparaat Hallo van Hallo cloud-naar-apparaat bericht toowhich deze stukje feedback betrekking heeft. |

Hallo-service moet opgeven een **MessageId** voor hello cloud-naar-apparaat message toobe kunnen toocorrelate de feedback met het oorspronkelijke Hallo-bericht.

Hallo ziet volgende voorbeeld Hallo berichttekst feedback.

```json
[
  {
    "OriginalMessageId": "0987654321",
    "EnqueuedTimeUtc": "2015-07-28T16:24:48.789Z",
    "StatusCode": 0,
    "Description": "Success",
    "DeviceId": "123",
    "DeviceGenerationId": "abcdefghijklmnopqrstuvwxyz"
  },
  {
    ...
  },
  ...
]
```

## <a name="cloud-to-device-configuration-options"></a>Configuratieopties voor cloud-naar-apparaat

Elke IoT-hub toont Hallo configuratieopties voor cloud-naar-apparaat messaging te volgen:

| Eigenschap                  | Beschrijving | Bereik en standaard |
| ------------------------- | ----------- | ----------------- |
| defaultTtlAsIso8601       | Standaard-TTL voor cloud-naar-apparaat-berichten. | Interval ISO_8601 up too2D (minimaal 1 minuut). Standaardwaarde: 1 uur. |
| maxDeliveryCount          | Levering van het maximum aantal voor cloud-naar-apparaat per apparaat wachtrijen. | 1 too100. Standaard: 10. |
| feedback.ttlAsIso8601     | Bewaren voor service-gebonden Feedbackberichten. | Interval ISO_8601 up too2D (minimaal 1 minuut). Standaardwaarde: 1 uur. |
| feedback.maxDeliveryCount |Levering van het maximum aantal voor feedbackwachtrij. | 1 too100. Standaard: 100. |

Voor meer informatie over hoe tooset deze configuratieopties zien [maken IoT hubs][lnk-portal].

## <a name="next-steps"></a>Volgende stappen

Voor informatie over het Hallo-SDK's kunt u berichten van tooreceive cloud-naar-apparaat gebruiken, Zie [Azure IoT SDK's][lnk-sdks].

tootry uit het ontvangen van berichten van de cloud-naar-apparaat, Zie Hallo [cloud naar apparaat verzenden] [ lnk-c2d-tutorial] zelfstudie.

[img-lifecycle]: ./media/iot-hub-devguide-messages-c2d/lifecycle.png

[lnk-portal]: iot-hub-create-through-portal.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-ttl]: #message-expiration-time-to-live
[lnk-c2d-configuration]: #cloud-to-device-configuration-options
[lnk-lifecycle]: #message-lifecycle
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
