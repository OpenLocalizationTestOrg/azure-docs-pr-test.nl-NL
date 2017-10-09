---
title: aaaUnderstand Azure IoT Hub apparaat-naar-cloud messaging | Microsoft Docs
description: Handleiding voor ontwikkelaars - hoe toouse apparaat-naar-cloud-berichten met IoT Hub. Bevat informatie over het verzenden van Telemetrie- en niet-telemtry gegevens en het gebruik van toodeliver routeren van berichten.
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
ms.openlocfilehash: 07dc8a6be747365c7efbc528ab2762b0d9790758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="send-device-to-cloud-messages-tooiot-hub"></a>Apparaat-naar-cloudberichten tooIoT Hub te verzenden

toosend tijdreeks Telemetrie en waarschuwingen van uw apparaten tooyour back-end oplossing, kunt u de apparaat-naar-cloud-berichten verzenden van uw apparaat tooyour IoT-hub. Zie voor een beschrijving van de andere ondersteund door de IoT Hub apparaat-naar-cloud-opties, [apparaat-naar-cloud communicatie richtlijnen][lnk-d2c-guidance].

U apparaat-naar-cloud-berichten verzenden via een apparaat gerichte-eindpunt (**/devices/ {deviceId} / berichten/gebeurtenissen**). Routering van regels en vervolgens uw berichten tooone Hallo service gerichte eindpunten op uw IoT-hub te routeren. Routeringsregels gebruiken Hallo kopteksten en de hoofdtekst van hello apparaat-naar-cloud-berichten die door uw hub toodetermine waar tooroute ze. Berichten zijn standaard gerouteerde toohello ingebouwde gerichte service-eindpunt (**berichten/gebeurtenissen**), die compatibel is met [Event Hubs][lnk-event-hubs]. Daarom kunt u standaard [Event Hubs-integratie en SDK's] [ lnk-compatible-endpoint] tooreceive apparaat-naar-cloud-berichten in uw oplossing voor back-end.

IoT Hub implementeert apparaat-naar-cloud-berichten met behulp van een streaming messaging-patroon. IoT-Hub apparaat-naar-cloudberichten lijken meer op [Event Hubs] [ lnk-event-hubs] *gebeurtenissen* dan [Service Bus] [ lnk-servicebus] *berichten* dat er wordt een groot aantal gebeurtenissen Hallo-service die kan worden gelezen door meerdere lezers te doorlopen.

Apparaat-naar-cloud-berichten met IoT Hub heeft Hallo volgende kenmerken:

* Apparaat-naar-cloud-berichten worden duurzame en bewaard in een IoT-hub standaard **berichten/gebeurtenissen** eindpunt voor tooseven dagen.
* Apparaat-naar-cloud-berichten kunnen niet groter zijn dan 256 KB en kunnen worden gegroepeerd in batches toooptimize verzendt. Batches mag hoogstens 256 KB.
* Zoals uitgelegd in Hallo [besturingselement toegang tooIoT Hub] [ lnk-devguide-security] gedeelte, IoT-Hub kunt per apparaat authenticatie en toegangsbeheer.
* IoT-Hub kunt u toocreate too10 aangepaste eindpunten. Berichten worden afgeleverd toohello eindpunten op basis van de routes geconfigureerd op uw IoT-hub. Zie voor meer informatie [routering regels](#routing-rules).
* IoT-Hub kunt miljoenen gelijktijdig verbonden apparaten (Zie [quota's en beperking][lnk-quotas]).
* IoT Hub is niet toegestaan voor het partitioneren van willekeurige. Apparaat-naar-cloud-berichten worden gepartitioneerd op basis van hun oorspronkelijke **deviceId**.

Zie voor meer informatie over de verschillen tussen Hallo IoT Hub en Event Hubs-services Hallo [vergelijking van Azure IoT Hub en Azure Event Hubs][lnk-comparison].

## <a name="send-non-telemetry-traffic"></a>Niet-telemetrie verkeer verzenden

Vaak bovendien tootelemetry gegevenspunten, apparaten verzenden van berichten en aanvragen die afzonderlijke uitvoering en verwerking in Hallo back-end oplossing vereisen. Bijvoorbeeld, back kritieke waarschuwingen die een specifieke actie in Hallo moeten activeren-end. U kunt eenvoudig schrijven een [routeringsregel] [ lnk-devguide-custom] toosend deze typen berichten tooan eindpunt dedicated tootheir verwerking op basis van een koptekst op het Hallo-bericht of een waarde in de hoofdtekst van Hallo-bericht.

Zie voor meer informatie over Hallo aanbevolen manier tooprocess dit kind van bericht Hallo [zelfstudie: hoe tooprocess IoT Hub apparaat-naar-cloud-berichten] [ lnk-d2c-tutorial] zelfstudie.

## <a name="route-device-to-cloud-messages"></a>Apparaat-naar-cloud-berichten rondsturen

U hebt twee opties voor routering apparaat-naar-cloudberichten tooyour back-end-apps:

* Gebruik Hallo ingebouwde [Event Hub-compatibele eindpunt] [ lnk-compatible-endpoint] tooenable back-end apps tooread Hallo apparaat-naar-cloud-berichten ontvangen door Hallo hub. toolearn over ingebouwde Event Hub-compatibele eindpunt hello, Zie [apparaat-naar-cloud-berichten lezen uit Hallo ingebouwd eindpunt][lnk-devguide-builtin].
* Gebruik Routering regels toosend berichten toocustom eindpunten in uw IoT-hub. Aangepaste eindpunten inschakelen voor uw back-end apps tooread apparaat-naar-cloud-berichten met Event Hubs, Service Bus-wachtrijen of Service Bus-onderwerpen. toolearn over Routering en aangepaste eindpunten, Zie [aangepaste eindpunten en routeringsregels gebruikt voor apparaat-naar-cloud-berichten][lnk-devguide-custom].

## <a name="anti-spoofing-properties"></a>Eigenschappen anti-adresvervalsing (spoofing)

tooavoid apparaat vervalsing in IoT Hub apparaat-naar-cloud-berichten stempels alle berichten met Hallo volgende eigenschappen:

* **ConnectionDeviceId**
* **ConnectionDeviceGenerationId**
* **ConnectionAuthMethod**

Hallo eerst twee bevatten Hallo **deviceId** en **generationId** Hallo die afkomstig zijn apparaat, conform [identiteit apparaateigenschappen][lnk-device-properties].

Hallo **ConnectionAuthMethod** eigenschap bevat een JSON-geserialiseerd object, hello volgende eigenschappen:

```json
{
  "scope": "{ hub | device}",
  "type": "{ symkey | sas}",
  "issuer": "iothub"
}
```

## <a name="next-steps"></a>Volgende stappen

Voor informatie over het Hallo-SDK's kunt u toosend apparaat-naar-cloud-berichten gebruiken, Zie [Azure IoT SDK's][lnk-sdks].

Hallo [aan de slag] [ lnk-get-started] zelfstudies ziet u hoe toosend apparaat-naar-cloud-berichten van gesimuleerde en fysieke apparaten. Zie voor meer details Hallo [proces IoT Hub apparaat-naar-cloud-berichten met behulp van routes] [ lnk-d2c-tutorial] zelfstudie.

[lnk-devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[lnk-devguide-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-comparison]: iot-hub-compare-event-hubs.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-get-started]: iot-hub-get-started.md

[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-servicebus]: http://azure.microsoft.com/documentation/services/service-bus/
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-compatible-endpoint]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
