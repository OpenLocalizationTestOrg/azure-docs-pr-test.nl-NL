---
title: aaaUnderstand hello querytaal Azure IoT Hub | Microsoft Docs
description: Handleiding voor ontwikkelaars - beschrijving van de SQL-achtige IoT Hub-querytaal Hallo gebruikt tooretrieve informatie over apparaat horende en taken van uw IoT-hub.
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 851a9ed3-b69e-422e-8a5d-1d79f91ddf15
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/17
ms.author: elioda
ms.openlocfilehash: 01a7c8ffdf44c6c27b834739d02c8fef1dd3d3fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-query-language-for-device-twins-jobs-and-message-routing"></a>Referentie - querytaal IoT Hub voor apparaat horende, taken en het routeren van berichten

IoT Hub biedt een krachtige SQL-achtige taal tooretrieve informatie met betrekking tot [apparaat horende] [ lnk-twins] en [taken][lnk-jobs], en [berichtroutering][lnk-devguide-messaging-routes]. Dit artikel biedt:

* Een inleiding toohello belangrijke functies van Hallo querytaal IoT Hub, en
* Hallo gedetailleerde omschrijving van Hallo-taal.

## <a name="get-started-with-device-twin-queries"></a>Aan de slag met apparaat twin query 's
[Apparaat horende] [ lnk-twins] kan willekeurige JSON-objecten bevatten als zowel labels en eigenschappen. IoT-Hub kunt u tooquery apparaat horende als een enkele JSON-document met alle apparaten twin informatie.
Stel bijvoorbeeld dat uw IoT hub apparaat horende hebben Hallo structuur te volgen:

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        "location": {
            "region": "US",
            "plant": "Redmond43"
        }
    },
    "properties": {
        "desired": {
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300
            },
            "$metadata": {
            ...
            },
            "$version": 4
        },
        "reported": {
            "connectivity": {
                "type": "cellular"
            },
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300,
                "status": "Success"
            },
            "$metadata": {
            ...
            },
            "$version": 7
        }
    }
}
```

IoT-Hub toont Hallo apparaat horende als een documentverzameling aangeroepen **apparaten**.
Hallo volgende query haalt dus Hallo hele set horende apparaten:

```sql
SELECT * FROM devices
```

> [!NOTE]
> [Azure IoT SDK's] [ lnk-hub-sdks] ondersteuning voor paginering van veel resultaten.

IoT-Hub kunt u tooretrieve apparaat horende filteren met willekeurig voorwaarden. Bijvoorbeeld:

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

haalt Hallo apparaat horende Hello **location.region** tag te ingesteld**VS**.
Booleaanse operators en rekenkundige vergelijkingen worden ondersteund, bijvoorbeeld

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

Hiermee haalt u alle apparaten horende zich in Hallo ons geconfigureerd toosend telemetrie minder vaak dan elke minuut. Voor uw gemak is het ook mogelijk toouse matrixconstanten Hello **IN** en **NIN** (niet-in) operators. Bijvoorbeeld:

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

alle apparaten horende die gerapporteerd Wi-Fi of bekabelde verbindingen opgehaald. Het is vaak nodig tooidentify alle apparaat horende die een bepaalde eigenschap bevatten. IoT Hub Hallo-functie ondersteunt `is_defined()` voor dit doel. Bijvoorbeeld:

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

alle apparaten horende waarmee Hallo opgehaald `connectivity` eigenschap gerapporteerd. Raadpleeg toohello [WHERE-component] [ lnk-query-where] sectie voor de volledige verwijzing Hallo Hallo filtermogelijkheden.

Groepering en aggregaties worden ook ondersteund. Bijvoorbeeld:

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

retourneert Hallo telling van Hallo apparaten in de status van elk telemetrie-configuratie.

```json
[
    {
        "numberOfDevices": 3,
        "status": "Success"
    },
    {
        "numberOfDevices": 2,
        "status": "Pending"
    },
    {
        "numberOfDevices": 1,
        "status": "Error"
    }
]
```

Hallo voorgaande voorbeeld ziet u een situatie waarin drie apparaten gerapporteerd geslaagde configuratie, twee Hallo configuration steeds toepast en een heeft een fout gerapporteerd.

### <a name="c-example"></a>C#-voorbeeld
Hallo queryfunctionaliteit die wordt blootgelegd door Hallo [C# service SDK] [ lnk-hub-sdks] in Hallo **RegistryManager** klasse.
Hier volgt een voorbeeld van een eenvoudige query:

```csharp
var query = registryManager.CreateQuery("SELECT * FROM devices", 100);
while (query.HasMoreResults)
{
    var page = await query.GetNextAsTwinAsync();
    foreach (var twin in page)
    {
        // do work on twin object
    }
}
```

Opmerking hoe Hallo **query** object is gemaakt met een paginagrootte (omhoog too1000) en vervolgens meerdere pagina's kunnen worden opgehaald door de aanroepende Hallo **GetNextAsTwinAsync** methoden meerdere keren.
Opmerking die queryobject Hallo beschrijft meerdere **volgende\***, afhankelijk van Hallo deserialisatie optie vereist door de query hello, zoals twin of taak apparaatobjecten, of gewoon JSON toobe gebruikt als u projecties.

### <a name="nodejs-example"></a>Node.js-voorbeeld
Hallo queryfunctionaliteit die wordt blootgelegd door Hallo [Azure IoT service SDK voor Node.js] [ lnk-hub-sdks] in Hallo **register** object.
Hier volgt een voorbeeld van een eenvoudige query:

```nodejs
var query = registry.createQuery('SELECT * FROM devices', 100);
var onResults = function(err, results) {
    if (err) {
        console.error('Failed toofetch hello results: ' + err.message);
    } else {
        // Do something with hello results
        results.forEach(function(twin) {
            console.log(twin.deviceId);
        });

        if (query.hasMoreResults) {
            query.nextAsTwin(onResults);
        }
    }
};
query.nextAsTwin(onResults);
```

Opmerking hoe Hallo **query** object is gemaakt met een paginagrootte (omhoog too1000) en vervolgens meerdere pagina's kunnen worden opgehaald door de aanroepende Hallo **nextAsTwin** methoden meerdere keren.
Opmerking die queryobject Hallo beschrijft meerdere **volgende\***, afhankelijk van Hallo deserialisatie optie vereist door de query hello, zoals twin of taak apparaatobjecten, of gewoon JSON toobe gebruikt als u projecties.

### <a name="limitations"></a>Beperkingen
> [!IMPORTANT]
> Apparaat horende queryresultaten, kunnen een paar minuten vertraging met opzicht toohello meest recente waarden bevatten. Als het uitvoeren van query's afzonderlijk apparaat horende door-id, het is altijd beter toouse Hallo apparaat twin API, die altijd bevat de meest recente waarden Hallo en hoger beperking limieten ophalen.

Op dit moment vergelijkingen bijvoorbeeld alleen tussen primitieve typen (geen objecten) worden ondersteund `... WHERE properties.desired.config = properties.reported.config` wordt alleen ondersteund als deze eigenschappen primitieve waarden hebben.

## <a name="get-started-with-jobs-queries"></a>Aan de slag met taken query 's
[Taken] [ lnk-jobs] bieden een manier tooexecute bewerkingen op sets van apparaten. Elk apparaat twin Hallo informatie bevat van Hallo taken waarvoor onderdeel in een verzameling met de naam is **taken**.
Logisch,

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        ...
    },
    "properties": {
        ...
    },
    "jobs": [
        {
            "deviceId": "myDeviceId",
            "jobId": "myJobId",
            "jobType": "scheduleTwinUpdate",
            "status": "completed",
            "startTimeUtc": "2016-09-29T18:18:52.7418462",
            "endTimeUtc": "2016-09-29T18:20:52.7418462",
            "createdDateTimeUtc": "2016-09-29T18:18:56.7787107Z",
            "lastUpdatedDateTimeUtc": "2016-09-29T18:18:56.8894408Z",
            "outcome": {
                "deviceMethodResponse": null
            }
        },
        ...
    ]
}
```

Deze verzameling is momenteel als waarop **devices.jobs** in Hallo querytaal IoT Hub.

> [!IMPORTANT]
> Op dit moment Hallo taken eigenschap nooit geretourneerd tijdens het opvragen van apparaat horende (dat wil zeggen, query's met ' apparaten'). Kan alleen worden benaderd rechtstreeks met query's met `FROM devices.jobs`.
>
>

Bijvoorbeeld: tooget alle taken (afgelopen en geplande) die invloed hebben op één apparaat, kunt u Hallo query te volgen:

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

Houd er rekening mee hoe deze query bevat Hallo apparaatspecifieke status (en mogelijk Hallo directe methode antwoord) van elke taak geretourneerd.
Het is ook mogelijk toofilter met willekeurige Booleaanse voorwaarden op alle objecteigenschappen in Hallo **devices.jobs** verzameling.
Bijvoorbeeld: Hallo query te volgen:

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

haalt alle voltooid apparaat twin update taken voor apparaat **myDeviceId** die zijn gemaakt na September 2016.

Het is ook mogelijk tooretrieve Hallo per apparaat resultaten van één taak.

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a>Beperkingen
Op dit moment wordt een query op **devices.jobs** bieden geen ondersteuning voor:

* Projecties, daarom alleen `SELECT *` is mogelijk.
* De voorwaarden die betrekking toohello apparaat twin in toevoeging toojob eigenschappen hebben (Zie Hallo voorgaande sectie).
* Uitvoeren van aggregaties, zoals count, avg, groeperen op.

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a>Aan de slag met de apparaat-naar-cloud bericht routes query-expressies

Met behulp van [apparaat-naar-cloud routes][lnk-devguide-messaging-routes], kunt u een IoT Hub toodispatch apparaat-naar-cloud-op basis van expressies geëvalueerd op basis van afzonderlijke berichten toodifferent-eindpunten berichten configureren.

Hallo route [voorwaarde] [ lnk-query-expressions] gebruikt Hallo dezelfde IoT Hub-querytaal als voorwaarden in twin en taak query's. Route voorwaarden worden geëvalueerd op Hallo berichtkoppen en hoofdtekst. Uw routering query-expressie is mogelijk alleen berichtkoppen alleen Hallo hoofdtekst van het bericht of beide headers bericht en berichttekst. IoT Hub wordt ervan uitgegaan dat een specifiek schema voor Hallo kopteksten en de berichttekst in, in volgorde tooroute berichten en Hallo volgende secties is beschreven wat er nodig is voor IoT Hub tooproperly route:

### <a name="routing-on-message-headers"></a>Routering op berichtkoppen

IoT Hub wordt ervan uitgegaan dat de volgende JSON-weergave van berichtkoppen voor berichtroutering Hallo:

```json
{
    "$messageId": "",
    "$enqueuedTime": "",
    "$to": "",
    "$expiryTimeUtc": "",
    "$correlationId": "",
    "$userId": "",
    "$ack": "",
    "$connectionDeviceId": "",
    "$connectionDeviceGenerationId": "",
    "$connectionAuthMethod": "",
    "$content-type": "",
    "$content-encoding": "",

    "userProperty1": "",
    "userProperty2": ""
}
```

Bericht Systeemeigenschappen worden voorafgegaan door Hallo `'$'` symbool.
Eigenschappen van de gebruiker worden altijd geopend met hun naam. Als de naam van een eigenschap toocoincide met een systeemeigenschap gebeurt (zoals `$to`), Hallo gebruikerseigenschap wordt opgehaald met de Hallo `$to` expressie.
U kunt altijd toegang hebt tot de eigenschap system Hallo met behulp van haakjes `{}`: u kunt bijvoorbeeld Hallo expressie gebruiken `{$to}` tooaccess Hallo systeemeigenschap `to`. Eigenschapnamen ophalen altijd Hallo overeenkomstige system-eigenschap.

Houd er rekening mee dat de namen van eigenschappen zijn niet hoofdlettergevoelig.

> [!NOTE]
> Alle berichteigenschappen zijn tekenreeksen. Eigenschappen, zoals beschreven in Hallo [ontwikkelaarshandleiding][lnk-devguide-messaging-format], zijn momenteel niet beschikbaar toouse in query's.
>

Als u bijvoorbeeld een `messageType` eigenschap, kunt u tooroute alle telemetrie tooone eindpunt en alle waarschuwingen tooanother eindpunt. U kunt Hallo na expressie tooroute Hallo telemetrie schrijven:

```sql
messageType = 'telemetry'
```

En Hallo expressie tooroute Hallo waarschuwingsberichten te volgen:

```sql
messageType = 'alert'
```

Booleaanse expressies en functies worden ook ondersteund. Met deze functie kunt u toodistinguish tussen ernstniveau worden weergegeven, bijvoorbeeld:

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

Raadpleeg toohello [expressie en voorwaarden] [ lnk-query-expressions] sectie voor Hallo volledige lijst van ondersteunde operatoren en functies.

### <a name="routing-on-message-bodies"></a>Routering op de berichttekst

IoT Hub kan alleen worden doorgestuurd op basis van de berichttekst inhoud als de berichttekst Hallo correct is gevormd JSON gecodeerd in UTF-8, UTF-16- of UTF-32. U moet Hallo-inhoudstype van het Hallo-bericht te instellen`application/json` en Hallo inhoud codering tooone Hallo UTF-coderingen in Hallo-bericht headers tooallow Hallo-bericht van IoT Hub tooroute op basis van de inhoud van Hallo ondersteund. Als een Hallo headers niet is opgegeven, wordt IoT-Hub niet geprobeerd tooevaluate een query-expressie met betrekking tot Hallo hoofdtekst tegen het Hallo-bericht. Als uw bericht is niet een JSON-bericht, of als het Hallo-bericht geeft geen Hallo inhoudstype en codering van inhoud, mag u nog steeds berichtroutering tooroute op basis van berichtkoppen Hallo Hallo-bericht.

U kunt `$body` in Hallo query-expressie tooroute Hallo-bericht. Kunt u de verwijzing naar een eenvoudige hoofdtekst, hoofdtekst matrixverwijzing of meerdere hoofdtekst verwijzingen in Hallo query-expressie. Uw query-expressie kunt ook een verwijzing instantie met een verwijzing van de header bericht combineren. Hallo hieronder vindt u bijvoorbeeld alle geldige query-expressies:

```sql
$body.message.Weather.Location.State = 'WA'
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.message.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a>Basisprincipes van een IoT Hub-query
Elke IoT Hub-query bevat van een geselecteerd en van clausules en door waar u optionele en GROUP BY componenten. Elke query wordt uitgevoerd op een verzameling van JSON-documenten, bijvoorbeeld apparaat horende. Hallo FROM-component geeft Hallo document verzameling toobe herhaald op (**apparaten** of **devices.jobs**). Vervolgens Hallo-filter in Hallo waarin component is toegepast. Met aggregaties, Hallo resultaten van deze stap worden gegroepeerd als opgegeven in de Hallo GROUP BY-component en voor elke groep een rij wordt gegenereerd zoals opgegeven in Hallo SELECT-component.

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a>FROM-component
Hallo **van < from_specification >** component kunt wordt ervan uitgegaan dat slechts twee waarden: **van apparaten**, tooquery apparaat horende, of **van devices.jobs**, tooquery taak per-apparaat meer informatie.

## <a name="where-clause"></a>WHERE-component
Hallo **waarbij < filter_condition >** component is optioneel. Hiermee wordt een of meer voorwaarden dat Hallo JSON-documenten in hello FROM verzameling moeten voldoen aan de toobe opgenomen als onderdeel van Hallo resultaat. Elk JSON-document moet worden geëvalueerd Hallo opgegeven voorwaarden te 'true' toobe in Hallo resultaat opgenomen.

Hallo toegestaan voorwaarden worden beschreven in de sectie [expressies en voorwaarden][lnk-query-expressions].

## <a name="select-clause"></a>SELECT-component
Hallo SELECT-component (**Selecteer < select_list >**) is verplicht en Hiermee geeft u de waarden die worden opgehaald uit het Hallo-query. Hiermee geeft u Hallo JSON waarden toobe toogenerate nieuwe JSON-objecten gebruikt.
Voor elk element van gefilterde (en desgewenst gegroepeerde) subset van hello FROM verzameling Hallo, Hallo Projectiefase wordt een nieuwe JSON-object worden geconstrueerd met Hallo opgegeven waarden in de SELECT-component Hallo gegenereerd.

Hieronder vindt u Hallo grammatica van Hallo SELECT-component:

```
SELECT [TOP <max number>] <projection list>

<projection_list> ::=
    '*'
    | <projection_element> AS alias [, <projection_element> AS alias]+

<projection_element> :==
    attribute_name
    | <projection_element> '.' attribute_name
    | <aggregate>

<aggregate> :==
    count()
    | avg(<projection_element>)
    | sum(<projection_element>)
    | min(<projection_element>)
    | max(<projection_element>)
```

waar **%{attribute_name/** tooany-eigenschap van Hallo JSON-document in hello FROM verzameling verwijst. Enkele voorbeelden van SELECT-component kunnen worden gevonden in Hallo [aan de slag met apparaat twin query's] [ lnk-query-getstarted] sectie.

Op dit moment selectie componenten anders dan **Selecteer \***  worden alleen ondersteund in cumulatieve query's in horende apparaten.

## <a name="group-by-clause"></a>GROUP BY-component
Hallo **GROUP BY < group_specification >** component is een optionele stap die kan worden uitgevoerd nadat de WHERE-component in Hallo Hallo-filter opgegeven en voordat Hallo projectie opgegeven in Hallo selecteren. Deze documenten op basis van de waarde van een kenmerk Hallo gegroepeerd. Deze groepen zijn gebruikte toogenerate geaggregeerd waarden zoals opgegeven in de SELECT-component Hallo.

Er is een voorbeeld van een GROUP BY-query:

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

Hallo formele syntaxis voor GROUP BY is:

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

waar **%{attribute_name/** tooany-eigenschap van Hallo JSON-document in hello FROM verzameling verwijst.

Op dit moment wordt Hallo GROUP BY-component alleen ondersteund bij het opvragen van horende apparaten.

## <a name="expressions-and-conditions"></a>Expressies en voorwaarden
Op een hoog niveau een *expressie*:

* Evalueert tooan exemplaar van een JSON-type (zoals Booleaanse waarde, getal, string, matrix of object), en
* Wordt gedefinieerd door het bewerken van gegevens die afkomstig zijn van Hallo apparaat JSON-document en constanten met ingebouwde operatoren en functies.

*Voorwaarden* expressies die tooa Booleaanse waarde evalueren zijn. Een constante anders dan Booleaanse waarde **true** wordt beschouwd als **false** (inclusief **null**, **niet-gedefinieerde**, een willekeurig exemplaar object of de matrix elke tekenreeks en duidelijk Hallo Booleaanse waarde **false**).

Hallo-syntaxis voor expressies is:

```
<expression> ::=
    <constant> |
    attribute_name |
    <function_call> |
    <expression> binary_operator <expression> |
    <create_array_expression> |
    '(' <expression> ')'

<function_call> ::=
    <function_name> '(' expression ')'

<constant> ::=
    <undefined_constant>
    | <null_constant>
    | <number_constant>
    | <string_constant>
    | <array_constant>

<undefined_constant> ::= undefined
<null_constant> ::= null
<number_constant> ::= decimal_literal | hexadecimal_literal
<string_constant> ::= string_literal
<array_constant> ::= '[' <constant> [, <constant>]+ ']'
```

Waarbij:

| Symbool | Definitie |
| --- | --- |
| %{attribute_name/ | Een eigenschap van JSON-document in Hallo Hallo **FROM** verzameling. |
| binary_operator | Een binaire operator die worden vermeld in Hallo [Operators](#operators) sectie. |
| functie_naam| Een functie die worden vermeld in Hallo [functies](#functions) sectie. |
| decimal_literal |Een float uitgedrukt in decimale notatie. |
| hexadecimal_literal |Een getal, uitgedrukt door Hallo tekenreeks '0 x' gevolgd door een reeks van hexadecimale cijfers. |
| string_literal |Letterlijke tekenreeks zijn vertegenwoordigd door een reeks van nul of meer Unicode-tekens of escapereeksen Unicode-tekenreeksen. Letterlijke tekenreeks zijn ingesloten in enkele aanhalingstekens (apostrof: ') of dubbele aanhalingstekens (aanhalingsteken: '). Hiermee heft toegestaan: `\'`, `\"`, `\\`, `\uXXXX` voor Unicode-tekens die zijn gedefinieerd door 4 hexadecimale cijfers. |

### <a name="operators"></a>Operators
Hallo operators volgende worden ondersteund:

| Familie | Operators |
| --- | --- |
| Rekenkundige bewerking |+,-,*,/,% |
| Logische |EN, OF NIET |
| Vergelijking |=, !=, <, >, <=, >=, <> |

### <a name="functions"></a>Functies
Tijdens het opvragen van horende en taken Hallo alleen ondersteund is functie:

| Functie | Beschrijving |
| -------- | ----------- |
| IS_DEFINED(Property) | Retourneert een Booleaanse waarde waarmee wordt aangegeven als Hallo eigenschap een waarde is toegewezen (met inbegrip van `null`). |

Routes voorwaarden worden Hallo na wiskundige functies ondersteund:

| Functie | Beschrijving |
| -------- | ----------- |
| ABS(x) | Retourneert Hallo absolute (positieve) waarde Hallo opgegeven numerieke expressie. |
| EXP(x) | Retourneert Hallo exponentiële waarde Hallo opgegeven numerieke expressie (e ^ x). |
| Power(x,y) | Retourneert de waarde van de opgegeven Hallo Hallo expressie toohello opgegeven power (x ^ y).|
| Square(x) | Retourneert Hallo vierkante Hallo opgegeven numerieke waarde. |
| CEILING(x) | Retourneert Hallo kleinste geheel getal groter dan of gelijk zijn aan om Hallo opgegeven numerieke expressie. |
| Floor(x) | Retourneert de grootste integer Hallo kleiner dan of gelijk toohello numerieke expressie opgegeven. |
| Sign(x) | Retourneert Hallo positieve (+ 1), nul (0) of minteken (-1) Hallo opgegeven numerieke expressie.|
| WORTEL(x) | Retourneert Hallo vierkante Hallo opgegeven numerieke waarde. |

Routes voorwaarden worden Hallo na type controleren en functies die ondersteund:

| Functie | Beschrijving |
| -------- | ----------- |
| AS_NUMBER | Converteert Hallo invoerreeks tooa getal. `noop`Als de invoer is een getal. `Undefined` als tekenreeks geen een getal vertegenwoordigt.|
| IS_ARRAY | Retourneert een Booleaanse waarde die aangeeft als Hallo type Hallo expressie opgegeven is een matrix. |
| IS_BOOL | Retourneert een Booleaanse waarde die aangeeft als Hallo type Hallo expressie opgegeven is een Booleaanse waarde. |
| IS_DEFINED | Retourneert een Booleaanse waarde die aangeeft of Hallo eigenschap een waarde is toegewezen. |
| IS_NULL | Retourneert een Booleaanse waarde die aangeeft als Hallo type Hallo expressie opgegeven is null. |
| IS_NUMBER | Retourneert een Booleaanse waarde die aangeeft als Hallo type Hallo expressie opgegeven is een getal. |
| IS_OBJECT | Retourneert een Booleaanse waarde die aangeeft als Hallo type Hallo expressie opgegeven is een JSON-object. |
| IS_PRIMITIVE | Retourneert een Booleaanse waarde waarmee wordt aangegeven als Hallo type Hallo opgegeven expressie is een primitief (string, Boolean, numerieke of `null`). |
| IS_STRING | Retourneert een Booleaanse waarde die aangeeft als Hallo type Hallo expressie opgegeven is een tekenreeks. |

Routes voorwaarden worden Hallo na tekenreeks-functies ondersteund:

| Functie | Beschrijving |
| -------- | ----------- |
| CONCAT(x,...) | Retourneert een tekenreeks die Hallo resultaat is van het samenvoegen van twee of meer tekenreekswaarden. |
| LENGTH(x) | Retourneert Hallo aantal tekens Hallo opgegeven tekenreeksexpressie.|
| LOWER(x) | Retourneert een tekenreeksexpressie na hoofdletter gegevens toolowercase converteren. |
| UPPER(x) | Retourneert een tekenreeksexpressie na kleine letter gegevens toouppercase converteren. |
| De SUBTEKENREEKS (tekenreeks, start [, lengte]) | Retourneert deel uit van een tekenreeksexpressie die begint bij Hallo opgegeven teken op nul gebaseerde positie en blijft toohello opgegeven lengte of toohello einde van de Hallo-tekenreeks. |
| INDEX_OF (tekenreeks, fragment) | Retourneert Hallo beginpositie van de eerste instantie Hallo van tweede tekenreeksexpressie Hallo binnen Hallo eerste opgegeven tekenreeksexpressie of -1 als het Hallo-tekenreeks is niet gevonden.|
| STARTS_WITH (x, y) | Retourneert een Booleaanse waarde die aangeeft of de eerste tekenreeksexpressie Hallo op de tweede met de Hallo begint. |
| ENDS_WITH (x, y) | Retourneert een Booleaanse waarde die aangeeft of de eerste tekenreeksexpressie Hallo Hallo tweede eindigt. |
| CONTAINS(x,y) | Retourneert een Booleaanse waarde die aangeeft of de eerste tekenreeksexpressie Hallo Hallo op de tweede bevat. |

## <a name="next-steps"></a>Volgende stappen
Meer informatie over hoe tooexecute query's in uw apps met behulp van [Azure IoT SDK's][lnk-hub-sdks].

[lnk-query-where]: iot-hub-devguide-query-language.md#where-clause
[lnk-query-expressions]: iot-hub-devguide-query-language.md#expressions-and-conditions
[lnk-query-getstarted]: iot-hub-devguide-query-language.md#get-started-with-device-twin-queries

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging-routes]: iot-hub-devguide-messages-read-custom.md
[lnk-devguide-messaging-format]: iot-hub-devguide-messages-construct.md
[lnk-devguide-messaging-routes]: ./iot-hub-devguide-messages-read-custom.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
