---
title: Azure IoT Hub-eindpunten aaaUnderstand | Microsoft Docs
description: Handleiding voor ontwikkelaars - naslaginformatie over IoT Hub apparaat gerichte en gerichte service-eindpunten.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 57ba52ae-19c6-43e4-bc6c-d8a5c2476e95
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 8647f15d2f2a050ad5799ea82f4d2d46db0dbec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-endpoints"></a>Referentie - eindpunten van IoT-Hub

## <a name="iot-hub-names"></a>Namen van de IoT-Hub

U vindt Hallo-naam van Hallo IoT-hub die als host fungeert voor uw eindpunten in de portal op Hallo Hallo **overzicht** blade. Standaard Hallo DNS-naam van een IoT-hub eruit: `{your iot hub name}.azure-devices.net`.

U kunt Azure DNS toocreate een aangepaste DNS-naam voor uw IoT-hub. Zie voor meer informatie [gebruik Azure DNS tooprovide aangepast domeininstellingen voor een Azure-service](../dns/dns-custom-domain.md#azure-iot).

## <a name="list-of-built-in-iot-hub-endpoints"></a>Lijst met ingebouwde IoT Hub-eindpunten

Azure IoT Hub is een multitenant-service die de functionaliteit toovarious actoren beschrijft. Hallo volgende diagram toont Hallo verschillende eindpunten die IoT-Hub toont.

![IoT Hub-eindpunten][img-endpoints]

Hallo volgende lijst beschrijft Hallo eindpunten:

* **Resourceprovider**. Hallo resourceprovider IoT-Hub toont een [Azure Resource Manager] [ lnk-arm] interface. Deze interface kunnen Azure-abonnement eigenaars toocreate en IoT-hubs en tooupdate IoT hub eigenschappen verwijderen. Eigenschappen van de IoT Hub reguleren [hub niveau beveiligingsbeleid][lnk-accesscontrol]in plaats van toodevice niveau access control en functionele opties voor cloud-naar-apparaat en apparaat-naar-cloud-berichten. Hallo resourceprovider IoT-Hub kunt u ook te[apparaat-id's exporteren][lnk-importexport].
* **Identiteiten Apparaatbeheer**. Elke IoT-hub toont een reeks HTTP REST-eindpunten toomanage apparaat-id's (maken, ophalen, bijwerken en verwijderen). [Apparaat-id's] [ lnk-device-identities] worden gebruikt voor verificatie en toegangsbeheer van apparaat.
* **Apparaatbeheer twin**. Elke IoT-hub toont een set van gerichte service HTTP REST-eindpunt tooquery en update [apparaat horende] [ lnk-twins] (update voor labels en eigenschappen).
* **Taken management**. Elke IoT-hub beschrijft een reeks gerichte service HTTP REST-eindpunt tooquery en beheren van [taken][lnk-jobs].
* **Apparaat-eindpunten**. Voor elk apparaat in het identiteitenregister Hallo toont IoT-Hub een set eindpunten:

  * *Apparaat-naar-cloud-berichten verzenden*. Een apparaat gebruikmaakt van dit eindpunt te[apparaat-naar-cloud-berichten verzenden][lnk-d2c].
  * *Cloud-naar-apparaat-berichten ontvangen*. Een apparaat gebruikmaakt van dit eindpunt tooreceive gericht [cloud-naar-apparaatberichten][lnk-c2d].
  * *Initiëren van bestandsuploads*. Een apparaat gebruikmaakt van dit eindpunt tooreceive een Azure Storage SAS-URI van IoT-Hub te[uploaden van een bestand][lnk-upload].
  * *Ophalen en bijwerken van twin apparaateigenschappen*. Een apparaat gebruikmaakt van dit eindpunt tooaccess de [apparaat twin][lnk-twins]van eigenschappen.
  * *Directe methodeaanvragen ontvangen*. Een apparaat gebruikmaakt van dit eindpunt toolisten voor [directe methode][lnk-methods]van aanvragen.

    Deze eindpunten beschikbaar worden gesteld met [protocollen MQTT v3.1.1][lnk-mqtt], HTTP 1.1 en [AMQP 1.0] [ lnk-amqp] protocollen. AMQP is ook beschikbaar via [WebSockets] [ lnk-websockets] op poort 443.

    Hallo apparaat horende en methoden eindpunten zijn alleen beschikbaar wanneer u Hallo [protocollen MQTT v3.1.1] [ lnk-mqtt] protocol.

* **Service-eindpunten**. Elke IoT-hub toont een set eindpunten voor uw back-end oplossing toocommunicate met uw apparaten. Met één uitzondering, deze eindpunten zijn alleen toegankelijk met Hallo [AMQP] [ lnk-amqp] protocol. Hallo-methode aanroepen eindpunt is toegankelijk via Hallo HTTP-protocol.
  
  * *Apparaat-naar-cloud-berichten ontvangen*. Dit eindpunt is compatibel met [Azure Event Hubs][lnk-event-hubs]. Een back-endservice kan worden gebruikt tooread hello [apparaat-naar-cloudberichten] [ lnk-d2c] verzonden door uw apparaten. U kunt aangepaste eindpunten maken op uw IoT-hub in toevoeging toothis ingebouwd eindpunt.
  * *Cloud-naar-apparaat-berichten verzenden en ontvangen van bevestigingen voor levering*. Deze eindpunten inschakelen in uw oplossing voor back-end-toosend betrouwbare [cloud-naar-apparaatberichten][lnk-c2d], en tooreceive Hallo bijbehorende bevestigingen voor levering of verlopen.
  * *Bestandsmeldingen ontvangen*. Dit eindpunt messaging kunt u meldingen van tooreceive wanneer uw apparaten is een bestand uploaden. 
  * *Directe aanroepen van de methode*. Dit eindpunt kunt u een back-endservice tooinvoke een [directe methode] [ lnk-methods] op een apparaat.
  * *Controle van gebeurtenissen ontvangstbewerkingen*. Dit eindpunt, kunt u tooreceive operations controle van gebeurtenissen als uw IoT hub is geconfigureerd tooemit ze. Zie voor meer informatie [IoT Hub operations bewaking][lnk-operations-mon].

Hallo [Azure IoT SDK's] [ lnk-sdks] beschreven Hallo verschillende manieren tooaccess deze eindpunten.

Alle eindpunten van IoT Hub gebruiken Hallo [TLS] [ lnk-tls] protocol en er is geen eindpunt ooit wordt weergegeven op niet-versleuteld/niet-beveiligde kanalen.

## <a name="custom-endpoints"></a>Aangepaste eindpunten

U kunt bestaande Azure-services in uw abonnement tooyour IoT hub tooact koppelen als eindpunten voor het routeren van berichten. Deze eindpunten fungeren als service-eindpunten en worden gebruikt als een PUT voor berichtroutes. Apparaten kunnen niet schrijven rechtstreeks toohello extra eindpunten. toolearn meer informatie over het berichtroutes, Zie Hallo developer guide vermelding op [verzenden en ontvangen berichten met iothub][lnk-devguide-messaging].

IoT Hub ondersteunt momenteel hello Azure-services als extra eindpunten te volgen:

* Event Hubs
* Service Bus-wachtrijen
* Service Bus-onderwerpen

IoT Hub moet schrijftoegang toothese service-eindpunten voor de routering toowork bericht. Als u uw eindpunten via hello Azure-portal configureert, worden de benodigde machtigingen Hallo toegevoegd voor u. Zorg ervoor dat u uw services toosupport Hallo verwacht doorvoer configureren. Wanneer u uw IoT-oplossing voor het eerst configureert, mag u toomonitor moet uw extra eindpunten en breng de gewenste wijzigingen voor de daadwerkelijke laadbewerking Hallo.

Als een bericht overeenkomt met meerdere routes dat alle toohello verwijzen hetzelfde eindpunt IoT Hub biedt bericht toothat eindpunt slechts één keer. U doet daarom niet nodig tooconfigure Ontdubbeling op uw Service Bus-wachtrij of onderwerp. In gepartitioneerde wachtrijen garandeert partitie affiniteit bericht bestellen.

> [!NOTE]
> Service Bus-wachtrijen en onderwerpen die worden gebruikt als IoT-hubeindpunten mag geen **sessies** of **detectie van dubbele** ingeschakeld. Als een van deze opties zijn ingeschakeld, Hallo-eindpunt wordt weergegeven als **onbereikbaar** in hello Azure-portal.

Zie voor Hallo limieten op Hallo aantal eindpunten die u kunt toevoegen, [quota's en beperking][lnk-devguide-quotas].

## <a name="field-gateways"></a>Veld gateways

In een IoT-oplossing een *veldgateway* tussen uw apparaten en de eindpunten van uw IoT-Hub. Het is doorgaans bevindt sluiten tooyour apparaten. Uw apparaten communiceren rechtstreeks met Hallo veldgateway met behulp van een protocol dat wordt ondersteund door Hallo-apparaten. Hallo veld gatewayserver verbindt tooan IoT-hubeindpunt via een protocol dat wordt ondersteund door de IoT Hub. Een veldgateway is mogelijk een specifiek apparaat of een laag energieniveau computer aangepaste gateway-software die wordt uitgevoerd.

U kunt [Azure IoT rand] [ lnk-iot-edge] tooimplement een veldgateway. IoT-rand biedt functionaliteit, zoals communicatie van meerdere apparaten op Hallo multiplex dezelfde IoT Hub-verbinding.

## <a name="next-steps"></a>Volgende stappen

Er zijn andere onderwerpen met naslaginformatie in deze handleiding voor ontwikkelaars van IoT-Hub:

* [IoT Hub-querytaal voor apparaat horende, taken en het routeren van berichten][lnk-devguide-query]
* [Quota's en beperking][lnk-devguide-quotas]
* [IoT Hub MQTT-ondersteuning][lnk-devguide-mqtt]

[lnk-iot-edge]: https://github.com/Azure/iot-edge

[img-endpoints]: ./media/iot-hub-devguide-endpoints/endpoints.png
[lnk-amqp]: https://www.amqp.org/
[lnk-mqtt]: http://mqtt.org/
[lnk-websockets]: https://tools.ietf.org/html/rfc6455
[lnk-arm]: ../azure-resource-manager/resource-group-overview.md
[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/

[lnk-tls]: https://tools.ietf.org/html/rfc5246


[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-accesscontrol]: iot-hub-devguide-security.md#access-control-and-permissions
[lnk-importexport]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-device-identities]: iot-hub-devguide-identity-registry.md
[lnk-upload]: iot-hub-devguide-file-upload.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md

[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[lnk-operations-mon]: iot-hub-operations-monitoring.md
