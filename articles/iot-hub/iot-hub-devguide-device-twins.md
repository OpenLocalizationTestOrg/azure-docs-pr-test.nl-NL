---
title: aaaUnderstand Azure IoT Hub apparaat horende | Microsoft Docs
description: Handleiding voor ontwikkelaars - apparaat gebruiken horende toosynchronize status en de configuratie van gegevens tussen IoT Hub en uw apparaten
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 8a3da072-a5bf-46e5-8de4-24cdbb2a03fa
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7dade18665108ed352ff3d18e864dc34f451bbf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-device-twins-in-iot-hub"></a>Begrijpen en gebruiken van apparaat horende in IoT-Hub
## <a name="overview"></a>Overzicht
*Apparaat horende* zijn JSON-documenten die apparaatgegevens van status (metagegevens, configuraties en voorwaarden) opslaan. IoT Hub persistente een apparaat twin voor elk apparaat dat u verbinding tooIoT Hub maakt. Dit artikel wordt beschreven:

* structuur van Hallo apparaat twin Hallo: *labels*, *gewenste* en *gerapporteerd eigenschappen*, en
* Hallo-bewerkingen die apparaat-apps en back-ends voor horende apparaten kunnen uitvoeren.

> [!NOTE]
> Apparaat horende zijn momenteel alleen toegankelijk vanaf apparaten die verbinding tooIoT Hub maken met Hallo MQTT-protocol. Raadpleeg toohello [MQTT ondersteuning] [ lnk-devguide-mqtt] artikel voor instructies over het tooconvert bestaande apparaat app toouse MQTT.
> 
> 

### <a name="when-toouse"></a>Wanneer toouse
Apparaat horende te gebruiken:

* Apparaatspecifieke metagegevens opslaan in de cloud Hallo. Bijvoorbeeld, de implementatielocatie van de van een machine snoep Hallo.
* Huidige status rapportgegevens zoals beschikbaar mogelijkheden en de voorwaarden van de app op uw apparaat. Bijvoorbeeld, een apparaat is verbonden tooyour IoT-hub over mobiel of Wi-Fi.
* Hallo-status van langlopende werkstromen tussen apparaattoepassing en back-endserver voor apps worden gesynchroniseerd. Wanneer een back-Hallo oplossing einde geeft aan nieuwe firmware versie tooinstall Hallo en Hallo apparaat app rapporten verschillende fasen van het updateproces Hallo Hallo is.
* De metagegevens van apparaten, de configuratie of de status opvragen.

Raadpleeg te[apparaat-naar-cloud communicatie richtlijnen] [ lnk-d2c-guidance] voor instructies over het gebruik van de gerapporteerde eigenschappen, apparaat-naar-cloud-berichten of bestand uploaden.
Raadpleeg te[Cloud-naar-apparaat communicatie richtlijnen] [ lnk-c2d-guidance] voor hulp bij het gebruik van eigenschappen van de gewenste rechtstreekse methoden of cloud-naar-apparaat-berichten.

## <a name="device-twins"></a>Apparaat horende
Apparaat horende apparaatgerelateerde gegevens opslaan die:

* Apparaat- en back-ends kunnen toosynchronize apparaat voorwaarden en configuratie gebruiken.
* Hallo back-end oplossing kunt tooquery gebruiken en langlopende bewerkingen zijn gericht.

Hallo levenscyclus van een apparaat-twin is gekoppeld toohello overeenkomt [apparaat-id][lnk-identity]. Apparaat horende worden impliciet gemaakt en verwijderd wanneer een nieuw apparaat-id is gemaakt of verwijderd uit IoT Hub.

Een apparaat-twin is een JSON-document met:

* **Labels**. Een gedeelte van Hallo JSON-document dat back-end oplossing Hallo kunt lezen van en schrijven naar. Labels zijn niet zichtbaar toodevice apps.
* **Eigenschappen van de gewenste**. Gebruikt samen met de eigenschappen van de gerapporteerde toosynchronize apparaatconfiguratie of voorwaarden. Gewenste eigenschappen kunnen alleen worden ingesteld door Hallo oplossing terug einde en kunnen worden gelezen door Hallo apparaattoepassing. Hallo apparaattoepassing kan ook worden gewaarschuwd in realtime van wijzigingen in de eigenschappen van Hallo gewenst.
* **Eigenschappen gerapporteerd**. Gebruikt samen met de gewenste eigenschappen toosynchronize apparaatconfiguratie of voorwaarden. Eigenschappen van de gerapporteerde kunnen Hallo apparaattoepassing kan alleen worden ingesteld en worden gelezen en opgevraagd door Hallo back-end oplossing.

Hallo-hoofdmap van Hallo apparaat twin JSON-document bevat tevens Hallo alleen-lezen eigenschappen van Hallo bijbehorende apparaat-id opgeslagen in Hallo [identiteitsregister][lnk-identity].

![][img-twin]

Hallo volgende voorbeeld ziet u een apparaat twin JSON-document:

        {
            "deviceId": "devA",
            "generationId": "123",
            "status": "enabled",
            "statusReason": "provisioned",
            "connectionState": "connected",
            "connectionStateUpdatedTime": "2015-02-28T16:24:48.789Z",
            "lastActivityTime": "2015-02-30T16:24:48.789Z",

            "tags": {
                "$etag": "123",
                "deploymentLocation": {
                    "building": "43",
                    "floor": "1"
                }
            },
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata" : {...},
                    "$version": 1
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": 55,
                    "$metadata" : {...},
                    "$version": 4
                }
            }
        }

In het hoofdobject hello, Hallo Systeemeigenschappen en containerobjecten voor `tags` en beide `reported` en `desired` eigenschappen. Hallo `properties` container bevat sommige alleen-lezen-elementen (`$metadata`, `$etag`, en `$version`) dat wordt beschreven in Hallo [twin Apparaatmetagegevens] [ lnk-twin-metadata] en [ Optimistische gelijktijdigheid] [ lnk-concurrency] secties.

### <a name="reported-property-example"></a>Voorbeeld van de gerapporteerde eigenschap
In het vorige voorbeeld Hallo Hallo apparaat twin bevat een `batteryLevel` eigenschap die is gerapporteerd door Hallo apparaattoepassing. Deze eigenschap maakt het mogelijk tooquery en werkt op apparaten die zijn gebaseerd op Hallo laatste gemelde accuniveau. Andere voorbeelden zijn Hallo apparaat app apparaat rapportagemogelijkheden of opties voor netwerkconnectiviteit.

> [!NOTE]
> Eigenschappen van de gerapporteerde vereenvoudigen scenario's waarbij Hallo back-end oplossing is geïnteresseerd in de laatste bekende waarde van een eigenschap Hallo. Gebruik [apparaat-naar-cloudberichten] [ lnk-d2c] als Hallo back-end oplossing tooprocess apparaattelemetrie in de vorm Hallo van reeksen voorzien van een tijdstempel gebeurtenissen, zoals een tijdreeks moet.

### <a name="desired-property-example"></a>Voorbeeld van de gewenste eigenschap
In het vorige voorbeeld Hallo Hallo `telemetryConfig` apparaat twin gewenst en gerapporteerde eigenschappen worden gebruikt door Hallo back-end oplossing en Hallo app toosynchronize Hallo telemetrie apparaatconfiguratie voor dit apparaat. Bijvoorbeeld:

1. Hallo back-end oplossing Hallo gewenst eigenschap met de Hallo desired configuratiewaarde ingesteld. Hier volgt Hallo-gedeelte van Hallo-document met Hallo gewenst eigenschap is ingesteld:
   
        ...
        "desired": {
            "telemetryConfig": {
                "sendFrequency": "5m"
            },
            ...
        },
        ...
2. Hallo apparaattoepassing ontvangt een melding van Hallo wijziging onmiddellijk als op Hallo eerst verbinding of geen verbinding. Hallo apparaattoepassing vervolgens verslag uitbrengt Hallo bijgewerkt configuration (of een foutconditie Hallo met `status` eigenschap). Hier volgt Hallo gedeelte Hallo gerapporteerd eigenschappen:
   
        ...
        "reported": {
            "telemetryConfig": {
                "sendFrequency": "5m",
                "status": "success"
            }
            ...
        }
        ...
3. Hallo back-end oplossing kunt bijhouden Hallo resultaten van de bewerking van de configuratie van Hallo op veel apparaten door [opvragen] [ lnk-query] horende apparaten.

> [!NOTE]
> Hallo voorgaande codefragmenten zijn voorbeelden, geoptimaliseerd voor de leesbaarheid van eenrichtingssessie tooencode de configuratie van een apparaat en de status ervan. IoT Hub afdwingen voor Hallo apparaat twin gewenst en eigenschappen in Hallo apparaat horende gerapporteerd niet met een specifiek schema.
> 
> 

U kunt horende toosynchronize langlopende bewerkingen zoals firmware-updates. Voor meer informatie over hoe toouse eigenschappen toosynchronize en bijhouden een langdurige bewerking op apparaten, Zie [gebruik gewenst eigenschappen tooconfigure apparaten][lnk-twin-properties].

## <a name="back-end-operations"></a>Back-end-bewerkingen
Hallo back-end oplossing is van invloed op Hallo apparaat twin Hallo volgt atomic bewerkingen, die toegankelijk is via HTTP met:

1. **Apparaat-twin ophalen met id**. Deze bewerking retourneert Hallo apparaat twin document, inclusief tags en gewenst, gerapporteerd, en Systeemeigenschappen.
2. **Gedeeltelijk bijwerken apparaat twin**. Deze bewerking kan Hallo oplossing voor back-end toopartially update Hallo tags of gewenste eigenschappen in een twin apparaat. Hallo gedeeltelijke update wordt uitgedrukt als een JSON-document dat wordt toegevoegd of updates van een eigenschap. Eigenschappen instellen te`null` worden verwijderd. Hallo volgende voorbeeld wordt een nieuwe gewenste eigenschap met de waarde `{"newProperty": "newValue"}`, overschrijft de bestaande waarde Hallo van `existingProperty` met `"otherNewValue"`, en verwijdert u `otherOldProperty`. Er worden geen andere wijzigingen aangebracht tooexisting gewenst eigenschappen of labels:
   
        {
            "properties": {
                "desired": {
                    "newProperty": {
                        "nestedProperty": "newValue"
                    },
                    "existingProperty": "otherNewValue",
                    "otherOldProperty": null
                }
            }
        }
3. **Gewenste eigenschappen vervangen**. Deze bewerking kunt Hallo oplossing voor back-end toocompletely overschrijven alle bestaande gewenste eigenschappen en vervangen door een nieuwe JSON-document voor `properties/desired`.
4. **Vervang labels**. Deze bewerking kunt Hallo oplossing voor back-end toocompletely overschrijven alle bestaande codes en vervangen door een nieuwe JSON-document voor `tags`.
5. **Dubbele meldingen ontvangen**. Deze bewerking kunt Hallo oplossing voor back-end toobe gewaarschuwd als Hallo twin is gewijzigd. toodo, uw IoT-oplossing moet een route toocreate en tooset Hallo gegevensbron gelijk te*twinChangeEvents*. Standaard geen twin meldingen worden verzonden, dat wil zeggen, geen dergelijke routes vooraf bestaan. Als wijzigingsratio Hallo te hoog is of om andere redenen, zoals interne fouten Hallo IoT Hub slechts één melding waarin alle wijzigingen kan verzenden. Dus als uw toepassing moet betrouwbare voor controle en logboekregistratie van alle tussenliggende statussen, nog steeds aanbevolen wordt dat u D2C berichten. Hallo twin Meldingsbericht bevat eigenschappen en hoofdtekst.

    - Eigenschappen

    | Naam | Waarde |
    | --- | --- |
    $content-type | application/json |
    $iothub-enqueuedtime |  Tijd waarop het Hallo-bericht is verzonden |
    $iothub-bericht-bron | twinChangeEvents |
    $content-codering | UTF-8 |
    deviceId | Hallo-apparaat-id |
    hubName | Naam van de IoT-Hub |
    operationTimestamp | [ISO8601] tijdstempel van bewerking |
    bericht-iothub-schema | deviceLifecycleNotification |
    opType | 'replaceTwin' of 'updateTwin' |

    Bericht Systeemeigenschappen worden voorafgegaan door Hallo `'$'` symbool.

    - Hoofdtekst
        
    Deze sectie bevat alle Hallo twin wijzigingen in een JSON-indeling. Hallo verschil dat deze alle twin secties kan bevatten, wordt Hallo dezelfde notatie als een patch: labels, properties.reported properties.desired en dat het Hallo '$metadata' elementen bevat. Bijvoorbeeld:
    ```
    {
        "properties": {
            "desired": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            },
            "reported": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            }
        }
    }
    ``` 

Alle voorgaande operations ondersteuning Hallo [optimistische gelijktijdigheid] [ lnk-concurrency] en vereisen Hallo **ServiceConnect** toestemming hebben, zoals gedefinieerd in Hallo [beveiliging ] [ lnk-security] artikel.

Bovendien toothese bewerkingen, Hallo oplossing een back-end kan:

* Query uitvoeren op Hallo apparaat horende Hallo met SQL-achtige [IoT Hub-querytaal][lnk-query].
* Bewerkingen uitvoeren op grote gegevenssets apparaat horende met [taken][lnk-jobs].

## <a name="device-operations"></a>Apparaatbewerkingen
Hallo apparaattoepassing is van invloed op Hallo apparaat twin met Hallo atomische bewerkingen te volgen:

1. **Ophalen van apparaat twin**. Deze bewerking retourneert Hallo apparaat twin document (inclusief tags en gewenste, gerapporteerd en Systeemeigenschappen) voor Hallo momenteel apparaat verbonden.
2. **De eigenschappen van de gerapporteerde gedeeltelijk bijwerken**. Deze bewerking kunt Hallo gedeeltelijke update Hallo eigenschappen van de momenteel verbonden apparaat Hallo gerapporteerd. Deze bewerking gebruikt Hallo bijwerken van dezelfde JSON-indeling die Hallo oplossing back-end gebruikt voor een gedeeltelijke update van de gewenste eigenschappen.
3. **Houd rekening met de eigenschappen van de gewenste**. Hallo momenteel aangesloten apparaat kunt toobe updates toohello gewenst eigenschappen van een melding krijgen wanneer ze zich voordoen. Hallo apparaat ontvangt Hallo hetzelfde formulier van update (gedeeltelijke of volledige vervanging) wordt uitgevoerd door Hallo back-end oplossing.

Alle voorgaande bewerkingen Hallo Hallo vereisen **DeviceConnect** toestemming hebben, zoals gedefinieerd in Hallo [beveiliging] [ lnk-security] artikel.

Hallo [apparaat Azure IoT SDK's] [ lnk-sdks] maken het gemakkelijk toouse Hallo voorafgaand aan de bewerkingen van veel talen en platforms. Meer informatie over het Hallo-details van IoT Hub primitieven voor synchronisatie van de gewenste eigenschappen vindt u in [apparaat opnieuw verbinden stroom][lnk-reconnection].

> [!NOTE]
> Apparaat horende zijn momenteel alleen toegankelijk vanaf apparaten die verbinding tooIoT Hub maken met Hallo MQTT-protocol.
> 
> 

## <a name="reference-topics"></a>De onderwerpen waarnaar wordt verwezen:
Hallo bieden volgende naslagonderwerpen u meer informatie over het beheren van toegang tooyour iothub.

## <a name="tags-and-properties-format"></a>Labels en eigenschappen indeling
Labels, gewenste en gerapporteerde eigenschappen zijn JSON-objecten met Hallo volgende beperkingen:

* Alle sleutels in JSON-objecten zijn hoofdlettergevoelig 64 bytes UTF-8, UNICODE-tekenreeksen. Toegestane tekens Unicode-tekens (segmenten C0 en C1), uitsluiten en `'.'`, `' '`, en `'$'`.
* Alle waarden in de JSON-objecten van de volgende JSON-typen Hallo kunnen zijn: boolean, getal, string, object. Matrices zijn niet toegestaan.
* Alle JSON-objecten in tags, gewenste en gerapporteerde eigenschappen kunnen een maximale diepte van 5 hebben. Bijvoorbeeld: Hallo na-object is ongeldig:

        {
            ...
            "tags": {
                "one": {
                    "two": {
                        "three": {
                            "four": {
                                "five": {
                                    "property": "value"
                                }
                            }
                        }
                    }
                }
            },
            ...
        }

* Alle tekenreekswaarden mag hoogstens 512 bytes lang.

## <a name="device-twin-size"></a>De grootte van de apparaat-twin
IoT Hub worden afgedwongen voor een beperking van de grootte van 8KB op Hallo van waarden van `tags`, `properties/desired`, en `properties/reported`, met uitzondering van alleen-lezen-elementen.
Hallo grootte wordt berekend door het tellen van alle tekens, met uitzondering van UNICODE-tekens (segmenten C0 en C1) en ruimte beheren `' '` wanneer deze buiten een tekenreeksconstante wordt weergegeven.
IoT Hub worden alle bewerkingen die Hallo van deze documenten boven hello vergroot zou geweigerd met een fout.

## <a name="device-twin-metadata"></a>Metagegevens van apparaten twin
IoT Hub onderhoudt Hallo tijdstempel van de laatste update Hallo voor elk JSON-object in de apparaat-twin gewenst en eigenschappen gerapporteerd. Hallo tijdstempels in UTC en gecodeerd in Hallo [ISO8601] indeling `YYYY-MM-DDTHH:MM:SS.mmmZ`.
Bijvoorbeeld:

        {
            ...
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": {
                                "$lastUpdated": "2016-03-30T16:24:48.789Z"
                            },
                            "$lastUpdated": "2016-03-30T16:24:48.789Z"
                        },
                        "$lastUpdated": "2016-03-30T16:24:48.789Z"
                    },
                    "$version": 23
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": "55%",
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": "5m",
                            "status": {
                                "$lastUpdated": "2016-03-31T16:35:48.789Z"
                            },
                            "$lastUpdated": "2016-03-31T16:35:48.789Z"
                        }
                        "batteryLevel": {
                            "$lastUpdated": "2016-04-01T16:35:48.789Z"
                        },
                        "$lastUpdated": "2016-04-01T16:24:48.789Z"
                    },
                    "$version": 123
                }
            }
            ...
        }

Deze informatie wordt opgeslagen op elk niveau (niet alleen Hallo leaves Hallo JSON-structuur) toopreserve updates objectsleutels te verwijderen.

## <a name="optimistic-concurrency"></a>Optimistische gelijktijdigheid
Labels, gewenst en eigenschappen van alle ondersteuning optimistische gelijktijdigheid gerapporteerd.
Labels hebben een ETag conform [RFC7232], die staat voor de JSON-weergave Hallo-tag. U kunt ETags gebruiken in voorwaardelijke bijwerkbewerkingen van Hallo oplossing voor back-end tooensure consistentie.

Apparaat-twin gewenst en gerapporteerde eigenschappen zijn niet ETags, maar hebben een `$version` waarde die kan worden gegarandeerd toobe incrementele. Tooan ETag, Hallo versie kan ook worden gebruikt door Hallo bijwerken van derden tooenforce consistentie van updates. Bijvoorbeeld, een apparaat-app voor een gerapporteerde eigenschap of Hallo back-end oplossing voor een gewenste eigenschap.

Versies zijn ook handig wanneer een observing agent (zoals Hallo apparaattoepassing Hallo gewenst eigenschappen observeren) op elkaar races tussen Hallo resultaat van een bewerking ophalen en een melding van updates afstemmen moet. sectie Hallo [apparaat opnieuw verbinden stroom] [ lnk-reconnection] vindt u meer informatie.

## <a name="device-reconnection-flow"></a>Opnieuw verbinden stroom van apparaat
IoT Hub behoudt updatemeldingen gewenste eigenschappen voor niet-verbonden apparaten niet. Hieruit volgt dat een apparaat dat verbinding maakt Hallo volledige gewenste eigenschappendocument in toevoeging toosubscribing voor updatemeldingen moet ophalen. Hallo races tussen updatemeldingen en volledige ophalen van de mogelijkheid gegeven, ervoor Hallo volgende stroom wordt gezorgd

1. App voor het apparaat verbindt tooan IoT-hub.
2. App voor het apparaat is lid voor de gewenste eigenschappen updatemeldingen.
3. Apparaattoepassing haalt Hallo volledige document voor gewenste eigenschappen.

Hallo apparaattoepassing kunt negeren alle meldingen met `$version` of minder zijn dan de versie van volledige opgehaalde document Hallo Hallo. Deze aanpak is mogelijk omdat IoT Hub wordt gegarandeerd dat versies altijd verhogen.

> [!NOTE]
> Deze logica wordt al geïmplementeerd in Hallo [apparaat Azure IoT SDK's][lnk-sdks]. Deze beschrijving is handig als Hallo apparaattoepassing een apparaat met Azure IoT SDK's gebruiken kan en Hallo MQTT interface moet rechtstreeks programma.
> 
> 

## <a name="additional-reference-material"></a>Aanvullende referentiemateriaal
Er zijn andere onderwerpen met naslaginformatie in Hallo Ontwikkelaarshandleiding voor IoT Hub:

* Hallo [IoT-hubeindpunten] [ lnk-endpoints] beschreven Hallo verschillende eindpunten die elke IoT-hub voor runtime- en beheerbewerkingen toont.
* Hallo [bandbreedtebeperking en quota's] [ lnk-quotas] Hallo quota's die van toepassing toohello service IoT Hub en bandbreedteregeling gedrag tooexpect Hallo wanneer u Hallo-service wordt beschreven.
* Hallo [apparaat en de service Azure IoT-SDK's] [ lnk-sdks] artikel lijsten Hallo verschillende taal SDK's kunt u bij het ontwikkelen van apps voor het apparaat en de service die communiceren met IoT Hub.
* Hallo [querytaal IoT Hub voor apparaat horende, taken en berichtroutering] [ lnk-query] beschreven Hallo querytaal IoT-Hub kunt u informatie van de tooretrieve uit IoT Hub over uw apparaat horende en taken .
* Hallo [IoT Hub MQTT ondersteuning] [ lnk-devguide-mqtt] artikel vindt u meer informatie over ondersteuning voor Hallo MQTT protocol IoT Hub.

## <a name="next-steps"></a>Volgende stappen
Nu u over horende apparaten hebt geleerd, kunt u mogelijk geïnteresseerd in de volgende onderwerpen voor IoT Hub developer guide Hallo:

* [Een directe methode aangeroepen voor een apparaat][lnk-methods]
* [Taken plannen op meerdere apparaten][lnk-jobs]

Als u tootry sommige Hallo concepten die in dit artikel wordt beschreven wilt, kunt u mogelijk geïnteresseerd in Hallo IoT Hub zelfstudies te volgen:

* [Hoe toouse Hallo apparaat twin][lnk-twin-tutorial]
* [Hoe toouse apparaat eigenschappen twin][lnk-twin-properties]

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-identity]: iot-hub-devguide-identity-registry.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-security]: iot-hub-devguide-security.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[ISO8601]: https://en.wikipedia.org/wiki/ISO_8601
[RFC7232]: https://tools.ietf.org/html/rfc7232
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-twin-metadata]: iot-hub-devguide-device-twins.md#device-twin-metadata
[lnk-concurrency]: iot-hub-devguide-device-twins.md#optimistic-concurrency
[lnk-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow

[img-twin]: media/iot-hub-devguide-device-twins/twin.png
