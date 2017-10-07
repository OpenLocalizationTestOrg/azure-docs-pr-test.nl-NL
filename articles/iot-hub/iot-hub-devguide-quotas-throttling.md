---
title: aaaUnderstand Azure IoT Hub quota en beperking | Microsoft Docs
description: Handleiding voor ontwikkelaars - beschrijving van het Hallo-quota's die van toepassing tooIoT Hub en Hallo verwacht bandbreedteregeling gedrag.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 425e1b08-8789-4377-85f7-c13131fae4ce
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 023fa29bfbfb1de35708d6d121a1c56b50adfed9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-quotas-and-throttling"></a>Referentie - IoT-Hub quota's en beperking

## <a name="quotas-and-throttling"></a>Quota en beperkingen
Elk Azure-abonnement kan maximaal 10 IoT hubs en maximaal 1 gratis hub hebben.

Elke IoT-hub is ingericht met een bepaald aantal eenheden in een specifieke SKU (Zie voor meer informatie [prijzen van Azure IoT Hub][lnk-pricing]). Hallo SKU en het aantal eenheden bepalen Hallo dagelijkse maximumquotum van berichten die u kunt verzenden.

Hallo SKU bepaalt ook Hallo beperking-limieten die IoT Hub worden afgedwongen voor alle bewerkingen.

## <a name="operation-throttles"></a>Bewerking vertragingen
Bewerking vertragingen zijn snelheid beperkingen die zijn toegepast in Hallo minuut bereiken en zijn bedoeld tooavoid misbruik. IoT Hub probeert tooavoid retourneert fouten indien mogelijk, maar deze wordt gestart met het retourneren van uitzonderingen als Hallo versnelling wordt geschonden te lang.

Hallo volgende tabel toont Hallo afgedwongen vertragingen. Waarden verwijzen tooan afzonderlijke hub.

| Vertragen | Gratis en S1 hubs | S2-hubs | S3-hubs | 
| -------- | ------- | ------- | ------- |
| Identiteit registerbewerkingen (maken, ophalen, weergeven, bijwerken en verwijderen) | 1.67/sec/Unit (min-100/unit) | 1.67/sec/Unit (min-100/unit) | 83.33/sec/Unit (min-5000/unit) |
| Apparaatverbindingen | Maximaal 100 per seconde of sec-12-eenheid <br/> Twee S1 eenheden zijn bijvoorbeeld 2\*12 = 24/sec, maar u hebt ten minste 100 per seconde voor uw units. Met negen S1 eenheden, hebt u 108 per seconde (9\*12) voor uw units. | sec-120-eenheid | sec-6000-eenheid |
| Apparaat-naar-cloud verzendt | Maximaal 100 per seconde of sec-12-eenheid <br/> Twee S1 eenheden zijn bijvoorbeeld 2\*12 = 24/sec, maar u hebt ten minste 100 per seconde voor uw units. Met negen S1 eenheden, hebt u 108 per seconde (9\*12) voor uw units. | sec-120-eenheid | sec-6000-eenheid |
| Cloud-naar-apparaat verzendt | 1.67/sec/Unit (min-100/unit) | 1.67/sec/Unit (min-100/unit) | 83.33/sec/Unit (min-5000/unit) |
| Cloud-naar-apparaat ontvangt <br/> (alleen als apparaat HTTP gebruikt)| 16.67/sec/Unit (min-1000/unit) | 16.67/sec/Unit (min-1000/unit) | 833.33/sec/Unit (min-50000/unit) |
| Bestand uploaden | 1.67 bestand uploaden meldingen/sec/eenheid (min-100/unit) | 1.67 bestand uploaden meldingen/sec/eenheid (min-100/unit) | 83.33 bestand uploaden meldingen/sec/eenheid (min-5000/unit) |
| Directe methoden | sec-20-eenheid | sec-60-eenheid | sec-3000-eenheid | 
| Apparaatdubbel leest | 10 per seconde | Maximaal 10 per seconde of sec-1-eenheid | sec-50-eenheid |
| Apparaatdubbel werkt bij | 10 per seconde | Maximaal 10 per seconde of sec-1-eenheid | sec-50-eenheid |
| Taakbewerkingen <br/> (maken, bijwerken, weergeven, verwijderen) | 1.67/sec/Unit (min-100/unit) | 1.67/sec/Unit (min-100/unit) | 83.33/sec/Unit (min-5000/unit) |
| Doorvoer van taken per apparaat bewerkingen | 10 per seconde | Maximaal 10 per seconde of sec-1-eenheid | sec-50-eenheid |

Het is belangrijk tooclarify die Hallo *apparaatverbindingen* versnelling beheerst Hallo snelheid waarmee nieuwe apparaatverbindingen worden met een IoT-hub gemaakt kunnen. Hallo *apparaatverbindingen* versnelling heeft geen betrekking op Hallo kunt u het maximale aantal gelijktijdig verbonden apparaten. Hallo versnelling is afhankelijk van Hallo aantal eenheden die zijn ingericht voor Hallo iothub.

Als u één eenheid S1 koopt, krijgt u bijvoorbeeld een vertraging van 100 verbindingen per seconde. Daarom tooconnect 100.000 apparaten, het duurt minimaal 1000 seconden (ongeveer 16 minuten). U kunt echter zo veel gelijktijdig verbonden apparaten als er apparaten zijn geregistreerd in het identiteitenregister hebben.

Voor een gedetailleerdere beschrijving van IoT Hub, beperking gedrag, Zie Hallo blogbericht [IoT-Hub bandbreedtebeperking en u][lnk-throttle-blog].

> [!NOTE]
> Op elk gewenst is mogelijk tooincrease quota's of limieten beperken door Hallo aantal ingerichte eenheden van IoT-hub te verhogen.
> 
> [!IMPORTANT]
> Bewerkingen in het systeemregister identiteit zijn bedoeld voor gebruik tijdens runtime in Apparaatbeheer en inrichting van scenario's. Lezen of bijwerken van een groot aantal apparaat-id's wordt ondersteund door [importeren en exporteren van taken][lnk-importexport].
> 
> 

## <a name="other-limits"></a>Andere limieten

IoT Hub worden afgedwongen andere operationele beperkingen:

| Bewerking | Limiet |
| --------- | ----- |
| Bestand uploaden URI 's | 10000 SAS-URI's kan worden uit voor een opslagaccount in één keer. <br/> Er kunnen 10 SAS URI's per apparaat tegelijk zijn uitgeschakeld. |
| Taken | Taakgeschiedenis worden too30 dagen bewaard <br/> Maximum aantal gelijktijdige taken is 1 (voor de vrije en S1, 5 (voor S2), 10 (voor S3). |
| Extra eindpunten | SKU betaald misschien hubs 10 extra eindpunten. Beschikbare SKU-hubs kunnen één extra eindpunt hebben. |
| Regels voor het bericht doorsturen | SKU betaald misschien hubs 100 routeringsregels. Beschikbare SKU-hubs misschien vijf routeringsregels. |
| Apparaat-naar-cloud-berichten | Maximale berichtgrootte van 256 KB |
| Messaging-cloud-naar-apparaat | Maximale berichtgrootte van 64 KB |
| Messaging-cloud-naar-apparaat | Maximaal aantal berichten voor de levering van in behandeling is 50 |

> [!NOTE]
> Op dit moment Hallo maximum aantal apparaten dat u verbinding kunt maken tooa één IoT-hub 500.000 is. Als u deze limiet tooincrease wilt, neem dan contact op met [Microsoft Support](https://azure.microsoft.com/support/options/).

## <a name="latency"></a>Latentie
IoT Hub streeft tooprovide lage latentie voor alle bewerkingen. Vervaldatum toonetwork voorwaarden en andere factoren onvoorspelbare garantie er een maximale latentie geen. Bij het ontwerpen van uw oplossing, moet u het volgende doen:

* Vermijd een veronderstellingen over Hallo maximale latentie van elke bewerking IoT Hub.
* Uw IoT-hub in hello Azure-regio die het dichtst tooyour apparaten inrichten.
* Overweeg het gebruik van Azure IoT rand tooperform latentie gevoelig operations Hallo-apparaat of op een gateway sluiten toohello-apparaat.

Meerdere IoT Hub-eenheden invloed op beperking zoals eerder beschreven, maar geen eventuele extra latentie voordelen of garanties bieden.
Als er onverwachte toename in latentie van de bewerking, neem dan contact op met [Microsoft Support](https://azure.microsoft.com/support/options/).

## <a name="next-steps"></a>Volgende stappen
Er zijn andere onderwerpen met naslaginformatie in deze handleiding voor ontwikkelaars van IoT-Hub:

* [Eindpunten van IoT-Hub][lnk-devguide-endpoints]
* [IoT Hub-querytaal voor apparaat horende, taken en het routeren van berichten][lnk-devguide-query]
* [IoT Hub MQTT-ondersteuning][lnk-devguide-mqtt]

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[lnk-throttle-blog]: https://azure.microsoft.com/blog/iot-hub-throttling-and-you/
[lnk-importexport]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities

[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
