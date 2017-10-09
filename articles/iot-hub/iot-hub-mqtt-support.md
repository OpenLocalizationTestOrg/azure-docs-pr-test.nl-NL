---
title: ondersteuning voor Azure IoT Hub MQTT aaaUnderstand | Microsoft Docs
description: Ontwikkelaars begeleiden - ondersteuning voor apparaten die verbinding maken gebruik van IoT Hub apparaat gerichte eindpunt tooan Hallo MQTT-protocol. Bevat informatie over ingebouwde ondersteuning voor protocollen MQTT in hello Azure IoT-apparaat-SDK's.
services: iot-hub
documentationcenter: .net
author: kdotchkoff
manager: timlt
editor: 
ms.assetid: 1d71c27c-b466-4a40-b95b-d6550cf85144
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: kdotchko
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e461687963138987acdf1f4e0e34c453744ea191
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="communicate-with-your-iot-hub-using-hello-mqtt-protocol"></a>Communiceren met uw iothub met Hallo MQTT protocol

IoT-Hub kunt u apparaten toocommunicate met Hallo Iothub apparaat eindpunten met Hallo [protocollen MQTT v3.1.1] [ lnk-mqtt-org] -protocol op poort 8883 of protocollen MQTT v3.1.1 via WebSocket-protocol op poort 443. IoT Hub is vereist voor alle communicatie toobe van het apparaat beveiligd met TLS/SSL (daarom IoT Hub biedt geen ondersteuning voor niet-beveiligde verbindingen via poort. 1883).

## <a name="connecting-tooiot-hub"></a>Verbinding maken met tooIoT Hub

Een apparaat Hallo MQTT protocol tooconnect tooan IoT-hub kunt gebruiken met behulp van Hallo-bibliotheken in Hallo [Azure IoT SDK's] [ lnk-device-sdks] of rechtstreeks via Hallo MQTT protocol.

## <a name="using-hello-device-sdks"></a>Hallo apparaat SDK's gebruiken

[Apparaat-SDK's] [ lnk-device-sdks] die ondersteuning Hallo MQTT protocol zijn beschikbaar voor Java, Node.js, C, C# en Python. Hallo apparaat-SDK's gebruiken Hallo standaard IoT Hub connection string tooestablish een verbinding tooan IoT-hub. toouse hello MQTT protocol Hallo client protocol parameter moet worden ingesteld te**MQTT**. Standaard verbinding Hallo apparaat-SKD's tooan IoT Hub met Hallo **CleanSession** vlag ingesteld te**0** en gebruik **QoS 1** voor uitwisseling van berichten met Hallo iothub.

Wanneer een apparaat is verbonden tooan IoT-hub, bieden Hallo apparaat-SKD's methoden waarmee Hallo toosend apparaatberichten tooand berichten ontvangen van een IoT-hub.

Hallo volgende tabel bevat koppelingen toocode voorbeelden voor elke taal die wordt ondersteund en geeft op Hallo parameter toouse tooestablish een verbinding tooIoT Hub met Hallo MQTT-protocol.

| Taal | Parameter protocol |
| --- | --- |
| [Node.js][lnk-sample-node] |Azure-iot-device-mqtt |
| [Java][lnk-sample-java] |IotHubClientProtocol.MQTT |
| [C][lnk-sample-c] |MQTT_Protocol |
| [C#][lnk-sample-csharp] |TransportType.Mqtt |
| [Python][lnk-sample-python] |IoTHubTransportProvider.MQTT |

### <a name="migrating-a-device-app-from-amqp-toomqtt"></a>Migreren van een apparaat-app van AMQP tooMQTT

Als u van Hallo gebruikmaakt [apparaat-SKD's][lnk-device-sdks], overschakelen via AMQP vereist tooMQTT Hallo protocol parameter in de initialisatie van de client Hallo wijzigen, zoals eerder gezegd.

Wanneer doet, moet u ervoor dat toocheck Hallo volgende items:

* AMQP retourneert fouten voor veel voorwaarden terwijl MQTT Hallo verbinding verbreekt. Als gevolg hiervan uw uitzonderingsverwerking logica mogelijk enkele wijzigingen.
* Hallo biedt geen ondersteuning voor protocollen MQTT *afwijzen* operations tijdens het ontvangen van [cloud-naar-apparaatberichten][lnk-messaging]. Als uw back-endserver voor apps tooreceive een reactie van apparaattoepassing hello moet, kunt u overwegen [methoden directe][lnk-methods].

## <a name="using-hello-mqtt-protocol-directly"></a>Hallo MQTT protocol direct gebruik te maken
Als een apparaat niet kan Hallo apparaat-SDK's, kan deze toohello openbaar apparaat eindpunten met Hallo MQTT protocol op poort 8883 nog steeds verbinding maken. In Hallo **CONNECT** Hallo na waarden moet worden gebruikt in pakket Hallo apparaat:

* Voor Hallo **ClientId** veld, gebruikt u Hallo **deviceId**.
* Voor Hallo **gebruikersnaam** veld `{iothubhostname}/{device_id}/api-version=2016-11-14`, waarbij {iothubhostname} is Hallo volledige CName van Hallo iothub.

    Bijvoorbeeld, als hello naam van uw IoT-hub is **contoso.azure devices.net** en als de naam van uw apparaat Hallo **MyDevice01**, Hallo volledige **gebruikersnaam** veld moet bevatten `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.
* Voor Hallo **wachtwoord** veld, gebruikt u een SAS-token. Hallo-indeling van SAS-token is Hallo Hallo dezelfde als voor zowel hello HTTP- en AMQP protocollen:<br/>`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.

    Voor meer informatie over het toogenerate SAS-tokens, Zie Hallo apparaat sectie [IoT Hub met behulp van beveiligingstokens][lnk-sas-tokens].

    Bij het testen, kunt u ook hello gebruiken [apparaat explorer] [ lnk-device-explorer] hulpprogramma tooquickly genereren van een SAS-token die u kunt kopiëren en plakken in uw eigen code in:

  1. Ga toohello **Management** tabblad **apparaat Explorer**.
  2. Klik op **SAS-Token** (top rechts).
  3. Op **SASTokenForm**, selecteert u uw apparaat in Hallo **DeviceID** vervolgkeuzelijst. Stel uw **TTL**.
  4. Klik op **genereren** toocreate uw token.

     Hallo SAS-token die wordt gegenereerd is deze structuur: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.

     onderdeel van dit token toouse als Hallo Hallo **wachtwoord** veld tooconnect met behulp van protocollen MQTT is: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.

MQTT verbinding maken met en pakketten verbreken, IoT-Hub geeft een gebeurtenis op Hallo **Operations Monitoring** kanaal met aanvullende informatie waarmee u kunt tootroubleshoot verbindingsproblemen.

### <a name="sending-device-to-cloud-messages"></a>Verzenden van apparaat-naar-cloud-berichten

Nadat u de verbinding is geslaagd, een apparaat kunt verzenden met het berichten tooIoT Hub met `devices/{device_id}/messages/events/` of `devices/{device_id}/messages/events/{property_bag}` als een **onderwerpnaam**. Hallo `{property_bag}` element kunt Hallo apparaat toosend berichten met aanvullende eigenschappen in een url-notatie. Bijvoorbeeld:

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> Dit `{property_bag}` element gebruikt Hallo dezelfde codering voor queryreeksen in Hallo HTTP-protocol.
>
>

Hallo apparaattoepassing kunt `devices/{device_id}/messages/events/{property_bag}` als Hallo **wordt de naam van onderwerp** toodefine *berichten wordt* toobe doorgestuurd als een bericht telemetrie.

- IoT Hub biedt geen ondersteuning voor QoS-2-berichten. Als een apparaat-app een bericht met publiceert **QoS 2**, IoT-Hub Hallo netwerkverbinding wordt gesloten.
- IoT Hub behouden berichten niet bewaard is gebleven. Als een apparaat een bericht met Hallo verzendt **behouden** vlag ingesteld too1, IoT-Hub toegevoegd Hallo **x-opt-behouden** toepassingsbericht eigenschap toohello. In dit geval wordt in plaats van de persistente Hallo behouden bericht, IoT-Hub wordt doorgegeven toohello back-end-app.
- IoT Hub ondersteunt slechts één actieve MQTT verbinding per apparaat. Alle nieuwe MQTT verbinding namens Hallo dezelfde apparaat-ID wordt IoT Hub toodrop Hallo bestaande verbinding.

Zie voor meer informatie [Messaging-handleiding voor ontwikkelaars][lnk-messaging].

### <a name="receiving-cloud-to-device-messages"></a>Cloud-naar-apparaat-berichten ontvangen

tooreceive berichten uit IoT Hub, een apparaat moet zich abonneren met `devices/{device_id}/messages/devicebound/#` als een **onderwerp Filter**. Hallo met meerdere niveaus jokertekens  **#**  in Hallo onderwerp Filter alleen tooallow apparaat tooreceive aanvullende eigenschappen in de onderwerpnaam Hallo Hallo wordt gebruikt. IoT Hub kan geen gebruik van Hallo Hallo  **#**  of **?** jokertekens voor het filteren van de onderliggende onderwerpen. Omdat in IoT Hub is niet algemeen pub sub messaging broker, ondersteunt deze alleen onderwerpnamen Hallo gedocumenteerd en onderwerp filters.

Hallo apparaat ontvangt geen berichten uit IoT Hub, totdat deze is geabonneerd tooits apparaatspecifieke eindpunt, vertegenwoordigd door Hallo `devices/{device_id}/messages/devicebound/#` onderwerp filter. Nadat een geslaagde abonnement is ingesteld, begint Hallo apparaat alleen cloud-naar-apparaat-berichten dat is verzonden tooit na Hallo Hallo abonnement ontvangen. Als het Hallo-apparaat verbinding maakt met **CleanSession** vlag ingesteld te**0**, Hallo abonnement over de verschillende sessies worden bewaard. In dit geval Hallo volgende keer dat deze verbinding met maakt **CleanSession 0** Hallo apparaat ontvangt openstaande berichten die zijn verzonden tooit terwijl er verbinding is verbroken. Als het Hallo-apparaat gebruikt **CleanSession** vlag ingesteld te**1** echter deze niet ontvangt berichten uit IoT Hub totdat ze tooits apparaat-eindpunt onderschrijft.

IoT Hub berichten met Hallo levert **onderwerpnaam** `devices/{device_id}/messages/devicebound/`, of `devices/{device_id}/messages/devicebound/{property_bag}` als er een berichteigenschappen. `{property_bag}`url-codering sleutel-waardeparen van berichteigenschappen bevat. Alleen de toepassingseigenschappen en de gebruiker instelbare eigenschappen (zoals **messageId** of **correlationId**) zijn opgenomen in de eigenschappenverzameling Hallo. Namen van de eigenschap System hebben Hallo voorvoegsel  **$** , toepassingseigenschappen Hallo oorspronkelijke eigenschapsnaam met geen voorvoegsel gebruiken.

Wanneer een apparaat-app op is geabonneerd tooa onderwerp met **QoS 2**, IoT-Hub verleent maximale QoS-niveau 1 in Hallo **SUBACK** pakket. Daarna biedt IoT Hub berichten toohello apparaat met behulp van QoS-1.

### <a name="retrieving-a-device-twins-properties"></a>Ophalen van de eigenschappen van een apparaat-twin

Eerst een apparaat is lid van te`$iothub/twin/res/#`, tooreceive Hallo bewerking antwoorden. Vervolgens verzendt een leeg bericht tootopic `$iothub/twin/GET/?$rid={request id}`, met de ingestelde waarde voor **aanvraag-id**. Hallo-service stuurt vervolgens een antwoordbericht met Hallo apparaat twin gegevens over onderwerp `$iothub/twin/res/{status}/?$rid={request id}`, met behulp van dezelfde Hallo  **aanvraag-id** als Hallo-aanvraag.

Aanvraag-id mag geldige waarde voor de waarde van een bericht eigenschap conform [messaging Ontwikkelaarshandleiding voor IoT-Hub][lnk-messaging], en de status wordt gevalideerd als een geheel getal.
antwoordtekst Hallo bevat Hallo sectie met eigenschappen van Hallo apparaat twin:

Hallo-hoofdtekst van Hallo identiteit registervermelding beperkt toohello 'Eigenschappen' lid, bijvoorbeeld:

        {
            "properties": {
                "desired": {
                    "telemetrySendFrequency": "5m",
                    "$version": 12
                },
                "reported": {
                    "telemetrySendFrequency": "5m",
                    "batteryLevel": 55,
                    "$version": 123
                }
            }
        }

Hallo statuscodes zijn:

|Status | Beschrijving |
| ----- | ----------- |
| 200 | Geslaagd |
| 429 | Te veel aanvragen (beperkt), conform [beperking IoT-Hub][lnk-quotas] |
| 5** | Server-fouten |

Zie voor meer informatie [Ontwikkelaarshandleiding voor apparaat horende][lnk-devguide-twin].

### <a name="update-device-twins-reported-properties"></a>Update apparaat twin gerapporteerd eigenschappen

Hallo hieronder wordt beschreven hoe een apparaat Hallo bijgewerkt gerapporteerd eigenschappen in Hallo apparaat twin in IoT-Hub:

1. Een apparaat moet eerst abonneren toohello `$iothub/twin/res/#` onderwerp tooreceive Hallo van bewerking reacties uit IoT Hub.

1. Een apparaat verzendt een bericht waarin Hallo apparaat twin update toohello `$iothub/twin/PATCH/properties/reported/?$rid={request id}` onderwerp. Dit bericht bevat een **aanvraag-id** waarde.

1. Hallo service en vervolgens verzendt een antwoordbericht met nieuwe ETag-waarde voor Hallo Hallo gemelde eigenschappen verzameling op onderwerp `$iothub/twin/res/{status}/?$rid={request id}`. Dit maakt gebruik van dezelfde Hallo antwoordbericht **aanvraag-id** als Hallo-aanvraag.

Hallo-bericht aanvraagtekst bevat een JSON-document, wat zorgt voor nieuwe waarden voor de gerapporteerde eigenschappen (geen andere eigenschap of metagegevens kan worden aangepast).
Elk lid in de JSON-document Hallo updates of Hallo overeenkomend lid in Hallo apparaat twin document toevoegen. Een ledenset te`null`, verwijderingen Hallo lid van Hallo dat object bevat. Bijvoorbeeld:

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

Hallo statuscodes zijn:

|Status | Beschrijving |
| ----- | ----------- |
| 200 | Geslaagd |
| 400 | Ongeldige aanvraag. Ongeldige JSON |
| 429 | Te veel aanvragen (beperkt), conform [beperking IoT-Hub][lnk-quotas] |
| 5** | Server-fouten |

Zie voor meer informatie [Ontwikkelaarshandleiding voor apparaat horende][lnk-devguide-twin].

### <a name="receiving-desired-properties-update-notifications"></a>Ontvangende gewenste eigenschappen updatemeldingen

Wanneer een apparaat is verbonden, IoT Hub verzendt meldingen toohello onderwerp `$iothub/twin/PATCH/properties/desired/?$version={new version}`, die inhoud Hallo Hallo update uitgevoerd door Hallo back-end oplossing bevatten. Bijvoorbeeld:

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

Als voor updates voor de eigenschap `null` waarden betekent dat Hallo JSON-object lid wordt verwijderd.


> [!IMPORTANT] 
> IoT Hub genereert wijzigingsmeldingen alleen wanneer apparaten zijn verbonden. Zorg ervoor dat tooimplement hello [apparaat opnieuw verbinden stroom] [ lnk-devguide-twin-reconnection] tookeep Hallo gewenst eigenschappen tussen IoT Hub en Hallo apparaattoepassing gesynchroniseerd.

Zie voor meer informatie [Ontwikkelaarshandleiding voor apparaat horende][lnk-devguide-twin].

### <a name="respond-tooa-direct-method"></a>Directe methode tooa reageren

Eerst een apparaat toosubscribe te heeft`$iothub/methods/POST/#`. IoT Hub verzendt methode aanvragen toohello onderwerp `$iothub/methods/POST/{method name}/?$rid={request id}`, met een geldige JSON of een lege hoofdtekst.

toorespond, Hallo apparaat verzendt een bericht met een geldige JSON of een lege hoofdtekst toohello onderwerp `$iothub/methods/res/{status}/?$rid={request id}`, waarbij **aanvraag-id** heeft toomatch Hallo in aanvraag het Hallo-bericht, en **status** toobe is een geheel getal .

Zie voor meer informatie [directe methode Ontwikkelaarshandleiding voor][lnk-methods].

### <a name="additional-considerations"></a>Aanvullende overwegingen

Als een definitieve overweging als u nodig hebt toocustomize hello MQTT protocol gedrag Hallo cloud-zijde, moet u nagaan Hallo [protocolgateway van Azure IOT] [ lnk-azure-protocol-gateway] waarmee u toodeploy hoge prestaties aangepaste protocol-gateway die rechtstreeks met IoT Hub-interfaces. Hello Azure IoT-protocolgateway kunt u toocustomize Hallo apparaat protocol tooaccommodate brownfield MQTT implementaties of andere aangepaste protocollen. Deze aanpak is echter vereist die u uitvoert en een aangepaste protocol-gateway werkt.

## <a name="next-steps"></a>Volgende stappen

toolearn meer informatie over het protocol van de protocollen MQTT hello, Zie Hallo [MQTT documentatie][lnk-mqtt-docs].

toolearn meer informatie over het plannen van de implementatie van uw IoT Hub, Zie:

* [Azure gecertificeerd voor de catalogus van IoT-apparaat][lnk-devices]
* [Ondersteuning voor aanvullende protocollen][lnk-protocols]
* [Vergelijken met Event Hubs][lnk-compare]
* [Schalen, HA en Noodherstel][lnk-scaling]

toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:

* [Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide]
* [Een apparaat simuleren met Azure IoT rand][lnk-iotedge]

[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-mqtt-org]: http://mqtt.org/
[lnk-mqtt-docs]: http://mqtt.org/documentation
[lnk-sample-node]: https://github.com/Azure/azure-iot-sdk-node/blob/master/device/samples/simple_sample_device.js
[lnk-sample-java]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device/samples/send-receive-sample/src/main/java/samples/com/microsoft/azure/iothub/SendReceive.java
[lnk-sample-c]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt
[lnk-sample-csharp]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device/samples
[lnk-sample-python]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device/samples
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-sas-tokens]: iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-devices]: https://catalog.azureiotsuite.com/
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-messaging]: iot-hub-devguide-messaging.md

[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-twin-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow
[lnk-devguide-twin]: iot-hub-devguide-device-twins.md
