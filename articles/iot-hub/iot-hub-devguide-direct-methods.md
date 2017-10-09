---
title: Azure IoT Hub aaaUnderstand directe methoden | Microsoft Docs
description: Handleiding voor ontwikkelaars - code voor gebruik rechtstreeks methoden tooinvoke op uw apparaten vanuit een app service.
services: iot-hub
documentationcenter: .net
author: nberdy
manager: timlt
editor: 
ms.assetid: 9f0535f1-02e6-467a-9fc4-c0950702102d
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d15d44a0c3e1d1cda1669c1ed011c2f932e3d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a>Begrijpen en direct methoden uit IoT Hub aanroepen
## <a name="overview"></a>Overzicht
IoT Hub, hebt u mogelijkheid tooinvoke rechtstreekse methoden op apparaten van Hallo cloud. Rechtstreekse methoden vertegenwoordigen een request-reply interactie met een apparaat vergelijkbare tooan HTTP aanroepen in dat ze slagen of mislukken onmiddellijk (na een door de gebruiker opgegeven time). Dit is nuttig voor scenario's waarin Hallo loop van de directe actie verschillend, afhankelijk van of Hallo apparaat kunnen toorespond, zoals een SMS wake-up tooa apparaat verzenden als een apparaat is offline (SMS wordt duurder dan een methodeaanroep van) is.

Elke methode apparaat gericht op één apparaat. [Taken] [ lnk-devguide-jobs] plannen methodeaanroep voor niet-verbonden apparaten en bieden een manier tooinvoke rechtstreekse methoden op meerdere apparaten.

Iedereen met **service verbinding** machtigingen voor IoT Hub kunnen een methode aangeroepen voor een apparaat.

### <a name="when-toouse"></a>Wanneer toouse
Methoden voor direct een reactie op aanvragen patroon volgen en zijn bedoeld voor communicaties die direct bevestiging van hun resultaat, meestal interactieve besturingselement van het Hallo-apparaat, bijvoorbeeld tooturn op een ventilator vereisen.

Raadpleeg te[Cloud-naar-apparaat communicatie richtlijnen] [ lnk-c2d-guidance] als u twijfelt tussen het gebruik van de eigenschappen van de gewenste directe methoden of cloud-naar-apparaat-berichten.

## <a name="method-lifecycle"></a>De levenscyclus van de methode
Rechtstreekse methoden op Hallo apparaat worden geïmplementeerd en is mogelijk nul of meer invoerwaarden in Hallo methode nettolading toocorrectly instantiëren. Aanroepen van een directe methode via een URI service gerichte (`{iot hub}/twins/{device id}/methods/`). Een apparaat ontvangt rechtstreekse methoden door een apparaat-specifieke MQTT onderwerp (`$iothub/methods/POST/{method name}/`). We kunnen op extra apparaten aan clientzijde netwerkprotocollen in toekomstige Hallo ondersteuning voor directe methoden.

> [!NOTE]
> Wanneer u een directe methode voor een apparaat aangeroepen, namen en waarden mogen alleen US-ASCII-afdrukbare alfanumerieke behalve aanwezig in de volgende set Hallo: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.
> 
> 

Directe methoden zijn synchrone en een slagen of mislukken na de time-outperiode hello (standaard: 30 seconden, instelbare up too3600 seconden). Directe methoden zijn nuttig in interactieve scenario's waar u een apparaat tooact als Hallo-apparaat online en ontvangende opdrachten is, zoals het inschakelen van een licht via een telefoon. In deze scenario's gewenste toosee een onmiddellijke slagen of mislukken zodat Hallo cloudservice zo snel mogelijk op Hallo resultaat kan reageren. Hallo-apparaat kan sommige berichttekst als gevolg van het Hallo-methode retourneren, maar het is niet vereist voor Hallo methode toodo zodat. Er is geen garantie op volgorde of eventuele semantiek gelijktijdigheid van taken op methodeaanroepen.

Directe methode zijn HTTP-only van Hallo cloud kant en MQTT alleen-lezen van Hallo apparaat kant.

Hallo-nettolading voor methodeaanvragen en antwoorden is een JSON-document van too8KB.

## <a name="reference-topics"></a>De onderwerpen waarnaar wordt verwezen:
Hallo bieden volgende naslagonderwerpen u meer informatie over het gebruik van rechtstreekse methoden.

## <a name="invoke-a-direct-method-from-a-back-end-app"></a>Aanroepen van een directe methode van een back-endserver voor apps
### <a name="method-invocation"></a>De methodeaanroep
Directe methode aanroepen op een apparaat zijn HTTP-aanroepen die bestaan uit:

* Hallo *URI* specifieke toohello apparaat (`{iot hub}/twins/{device id}/methods/`)
* Hallo POST *methode*
* *Headers* waarop Hallo autorisatie bevatten, aanvraag-ID, het type inhoud en de codering van inhoud
* Een transparante JSON *hoofdtekst* in Hallo volgende indeling:

```
{
    "methodName": "reboot",
    "responseTimeoutInSeconds": 200,
    "payload": {
        "input1": "someInput",
        "input2": "anotherInput"
    }
}
```

Er is een time-out in seconden. Als u time-out niet is ingesteld, wordt standaard too30 seconden.

### <a name="response"></a>Antwoord
Hallo back-end app ontvangt een antwoord dat bestaat uit:

* *HTTP-statuscode*, die wordt gebruikt voor fouten die afkomstig zijn van Hallo IoT Hub, met inbegrip van een 404-fout voor apparaten die momenteel niet verbonden
* *Headers* waarop Hallo ETag bevatten, aanvraag-ID, het type inhoud en de codering van inhoud
* Een JSON *hoofdtekst* in Hallo volgende indeling:

```
{
    "status" : 201,
    "payload" : {...}
}
```

   Beide `status` en `body` worden geleverd door het Hallo-apparaat en toorespond gebruikt met de statuscode van Hallo van het apparaat en/of beschrijving.

## <a name="handle-a-direct-method-on-a-device"></a>Verwerken van een directe methode op een apparaat
### <a name="method-invocation"></a>De methodeaanroep
Apparaten ontvangen directe methode-aanvragen op Hallo MQTT onderwerp:`$iothub/methods/POST/{method name}/?$rid={request id}`

Hallo hoofdtekst welk apparaat Hallo ontvangt heeft Hallo volgende indeling:

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

Methodeaanvragen zijn QoS 0.

### <a name="response"></a>Antwoord
Hallo apparaat verzendt reacties te`$iothub/methods/res/{status}/?$rid={request id}`, waarbij:

* Hallo `status` eigenschap Hallo apparaat opgegeven status van de uitvoering van de methode is.
* Hallo `$rid` eigenschap Hallo aanvraag-ID van de methodeaanroep Hallo ontvangen van IoT Hub is.

Hallo-instantie is ingesteld door Hallo-apparaat en elke status kunt worden.

## <a name="additional-reference-material"></a>Aanvullende referentiemateriaal
Er zijn andere onderwerpen met naslaginformatie in Hallo Ontwikkelaarshandleiding voor IoT Hub:

* [IoT-hubeindpunten] [ lnk-endpoints] beschrijft Hallo verschillende eindpunten die elke IoT-hub voor runtime- en beheerbewerkingen toont.
* [Bandbreedtebeperking en quota's] [ lnk-quotas] beschrijft Hallo quota's die van toepassing toohello service IoT Hub en bandbreedteregeling gedrag tooexpect Hallo wanneer u Hallo-service gebruiken.
* [Azure IoT-SDKs voor apparaat en de service] [ lnk-sdks] lijsten Hallo verschillende taal kunt u bij het ontwikkelen van apps voor het apparaat en de service die communiceren met IoT Hub SDK's.
* [IoT Hub-querytaal voor apparaat horende, taken en berichtroutering] [ lnk-query] Hallo querytaal IoT-Hub kunt u informatie van de tooretrieve uit IoT Hub over uw apparaat horende en taken worden beschreven.
* [Ondersteuning voor IoT Hub MQTT] [ lnk-devguide-mqtt] meer informatie over IoT Hub ondersteuning biedt voor Hallo MQTT protocol.

## <a name="next-steps"></a>Volgende stappen
Nu hebt u geleerd hoe toouse direct methoden, hebt u mogelijk geïnteresseerd in Hallo IoT Hub developer guide onderwerp te volgen:

* [Taken plannen op meerdere apparaten][lnk-devguide-jobs]

Als u tootry sommige Hallo concepten die in dit artikel wordt beschreven wilt, kunt u mogelijk geïnteresseerd in Hallo IoT Hub-zelfstudie:

* [Directe methoden gebruiken][lnk-methods-tutorial]

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-messages]: iot-hub-devguide-messaging.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
