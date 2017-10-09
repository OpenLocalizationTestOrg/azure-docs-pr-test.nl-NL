---
title: aaaOverview Hallo Azure Relay knooppunt API's | Microsoft Docs
description: Relay-knooppunt API-overzicht
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b7d6e822-7c32-4cb5-a4b8-df7d009bdc85
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: d231acc854be0eaa965dec0229cf63b08ff27067
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="relay-hybrid-connections-node-api-overview"></a>Relay-hybride verbindingen knooppunt API-overzicht

## <a name="overview"></a>Overzicht

Hallo [ `hyco-ws` ](https://www.npmjs.com/package/hyco-ws) knooppunt-pakket voor Azure Relay hybride verbindingen is gebaseerd op en breidt Hallo ['ws'](https://www.npmjs.com/package/ws) NPM-pakket. Dit pakket opnieuw exporteert uitvoer van dat base pakket en voegt nieuwe uitvoer die integratie met de functie hybride verbindingen hello Azure Relay-service inschakelen. 

Bestaande toepassingen die `require('ws')` kunt dit pakket met `require('hyco-ws')` in plaats daarvan ook waardoor hybride scenario's waarin een toepassing kunt luisteren voor WebSocket-verbindingen lokaal uit 'binnen de firewall Hallo' en via de hybride verbindingen, alles op Hallo dezelfde tijd.
  
## <a name="documentation"></a>Documentatie

Hallo-API's zijn [gedocumenteerd in Hallo belangrijkste ws pakket](https://github.com/websockets/ws/blob/master/doc/ws.md). Dit artikel wordt beschreven hoe dit pakket verschilt van die basislijn. 

Hallo belangrijke verschillen tussen Hallo base pakket en deze 'hyco ws' is dat het een nieuwe serverklasse, geëxporteerd toevoegt `require('hyco-ws').RelayedServer`, en een aantal methoden.

### <a name="package-helper-methods"></a>Pakket Help-methoden

Er zijn verschillende hulpprogrammamethoden beschikbaar op Hallo pakket exporteren die u kunt verwijzen naar als volgt:

```JavaScript
const WebSocket = require('hyco-ws');

var listenUri = WebSocket.createRelayListenUri('namespace.servicebus.windows.net', 'path');
listenUri = WebSocket.appendRelayToken(listenUri, 'ruleName', '...key...')
...

```

Hallo helpmethoden zijn voor gebruik met dit pakket, maar kunnen ook worden gebruikt door de server van een knooppunt voor het inschakelen van web- of clients toocreate listeners of afzenders. Hallo-server gebruikt deze methoden door het doorgeven van URI's waarvan de tijdelijke tokens insluiten. Deze URI's kan ook worden gebruikt met algemene WebSocket-stacks die instelling HTTP-headers niet Hallo WebSocket-handshake ondersteunen. Autorisatie tokens insluiten in Hallo die URI hoofdzakelijk voor deze bibliotheek-externe gebruiksscenario's wordt ondersteund. 

#### <a name="createrelaylistenuri"></a>createRelayListenUri

```JavaScript
var uri = createRelayListenUri([namespaceName], [path], [[token]], [[id]])
```

Maakt een geldig Azure Relay hybride verbinding listener URI voor Hallo opgegeven naamruimte en het pad. Deze URI kan vervolgens worden gebruikt met Hallo relay-versie van Hallo WebSocketServer klasse.

- `namespaceName`(vereist) - domein gekwalificeerde naam van hello Azure Relay naamruimte toouse Hallo.
- `path`(vereist) - naam van een bestaande hybride verbinding van een Azure-Relay in die naamruimte Hallo.
- `token`(optioneel): een eerder uitgegeven relaytoegang token die is ingesloten in Hallo listener URI (Zie het volgende voorbeeld Hallo).
- `id`(optioneel): een tracerings-id end-to-end diagnostische tracering van aanvragen.

Hallo `token` waarde is optioneel en mag alleen worden gebruikt wanneer het niet mogelijk toosend HTTP-headers samen met de WebSocket-handshake hello, zoals Hallo geval met Hallo W3C WebSocket-stack.                  


#### <a name="createrelaysenduri"></a>createRelaySendUri
 
```JavaScript
var uri = createRelaySendUri([namespaceName], [path], [[token]], [[id]])
```

Hiermee maakt u een geldige Azure Relay hybride verbinding verzenden URI voor Hallo opgegeven naamruimte en het pad. Deze URI kan worden gebruikt met een WebSocket-client.

- `namespaceName`(vereist) - domein gekwalificeerde naam van hello Azure Relay naamruimte toouse Hallo.
- `path`(vereist) - naam van een bestaande hybride verbinding van een Azure-Relay in die naamruimte Hallo.
- `token`(optioneel): een eerder uitgegeven Relay toegangstoken dat is ingesloten in Hallo URI verzenden (Zie het volgende voorbeeld Hallo).
- `id`(optioneel): een tracerings-id end-to-end diagnostische tracering van aanvragen.

Hallo `token` waarde is optioneel en mag alleen worden gebruikt wanneer het niet mogelijk toosend HTTP-headers samen met de WebSocket-handshake hello, zoals Hallo geval met Hallo W3C WebSocket-stack.                   


#### <a name="createrelaytoken"></a>createRelayToken 

```JavaScript
var token = createRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

Hiermee maakt u een Azure Relay Shared Access Signature (SAS)-token voor Hallo opgegeven doel-URI, SAS-regel en SAS-sleutel voor regel die geldig is voor Hallo aantal seconden of een uur wordt gegeven van de huidige Hallo instant als Hallo verstrijken argument wordt weggelaten.

- `uri`(vereist) - URI voor welke Hallo-token uitgegeven toobe is Hallo. Hallo-URI is genormaliseerde toouse Hallo HTTP-schema en querygegevens tekenreeks wordt verwijderd.
- `ruleName`(vereist) - SAS-Regelnaam voor beide dat wordt vertegenwoordigd door de opgegeven URI Hallo Hallo-entiteit of voor Hallo naamruimte dat wordt vertegenwoordigd door Hallo hostgedeelte URI.
- `key`(vereist) - geldige sleutel voor Hallo SAS-regel. 
- `expirationSeconds`(optioneel): het aantal seconden totdat Hallo gegenereerd token Hallo moet verlopen. Als niet wordt opgegeven, is standaard Hallo 1 uur (3600).

Hallo uitgegeven token verleent Hallo rechten die zijn gekoppeld aan Hallo opgegeven SAS-regel voor Hallo opgegeven duur.

#### <a name="appendrelaytoken"></a>appendRelayToken

```JavaScript
var uri = appendRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

Deze methode is functioneel equivalent toohello `createRelayToken` methode eerder beschreven, maar retourneert Hallo token correct toegevoegde toohello invoer-URI.

### <a name="class-wsrelayedserver"></a>Klasse ws. RelayedServer

Hallo `hycows.RelayedServer` klasse is een alternatieve toohello `ws.Server` klasse die luistert niet op het lokale netwerk hello, maar delegeert luisterende toohello Azure Relay-service.

Hallo twee klassen zijn voornamelijk contract die compatibel zijn, wat betekent dat een bestaande toepassing hello met `ws.Server` klasse kan eenvoudig worden gewijzigd toouse Hallo relayed versie. de belangrijkste verschillen Hallo zijn in de constructor Hallo en Hallo beschikbare opties.

#### <a name="constructor"></a>Constructor  

```JavaScript 
var ws = require('hyco-ws');
var server = ws.RelayedServer;

var wss = new server(
    {
        server: ws.createRelayListenUri(ns, path),
        token: function() { return ws.createRelayToken('http://' + ns, keyrule, key); }
    });
```

Hallo `RelayedServer` constructor biedt ondersteuning voor een andere set argumenten dan Hallo `Server`, omdat het is niet een zelfstandige listener of kunnen toobe ingesloten in een bestaande HTTP-listener-framework. Er zijn ook minder mogelijkheden beschikbaar aangezien Hallo WebSocket management grotendeels gedelegeerd toohello Relay-service.

Constructor-argumenten:

- `server`(vereist) - gekwalificeerde Hallo volledig URI voor de naam van een hybride verbinding op welke toolisten, meestal met Hallo WebSocket.createRelayListenUri() Help-methode wordt gemaakt.
- `token`Dit argument is (vereist) - bevat een eerder uitgegeven token tekenreeks of een callback-functie die een token tekenreeks tooobtain kan worden aangeroepen. Hallo callback optie verdient de voorkeur, zoals kunnen de vernieuwing van het token.

#### <a name="events"></a>Gebeurtenissen

`RelayedServer`exemplaren verzenden drie gebeurtenissen die u toohandle binnenkomende aanvragen inschakelen, verbindingen tot stand brengen en foutcondities detecteren. U moet zich abonneren toohello `connect` toohandle gebeurtenisberichten. 

##### <a name="headers"></a>Headers

```JavaScript 
function(headers)
```

Hallo `headers` gebeurtenis wordt geactiveerd vlak voordat een binnenkomende verbinding is geaccepteerd, wijziging van Hallo headers toosend toohello client inschakelen. 

##### <a name="connection"></a>verbinding

```JavaScript
function(socket)
```

Verzonden wanneer een nieuwe WebSocket-verbinding is geaccepteerd. Hallo-object is van het type `ws.WebSocket`, net als met base Hallo-pakket.


##### <a name="error"></a>error

```JavaScript
function(error)
```

Als de onderliggende Hallo-server verzendt een fout opgetreden, is deze hier doorgestuurd.  

#### <a name="helpers"></a>Hulpprogramma 's

toosimplify vanaf een relayed server en onmiddellijk abonneren tooincoming verbindingen, Hallo van het pakket wordt een eenvoudige Help-functie, die ook wordt gebruikt in de voorbeelden hello, als volgt:

##### <a name="createrelayedlistener"></a>createRelayedListener

```JavaScript
var WebSocket = require('hyco-ws');

var wss = WebSocket.createRelayedServer(
    {
        server: WebSocket.createRelayListenUri(ns, path),
        token: function() { return WebSocket.createRelayToken('http://' + ns, keyrule, key); }
    }, 
    function (ws) {
        console.log('connection accepted');
        ws.onmessage = function (event) {
            console.log(JSON.parse(event.data));
        };
        ws.on('close', function () {
            console.log('connection closed');
        });       
});
``` 

##### <a name="createrelayedserver"></a>createRelayedServer

```javascript
var server = createRelayedServer([options], [connectCallback] )
```

Deze methode aanroept Hallo constructor toocreate een nieuw exemplaar van Hallo RelayedServer en vervolgens Hallo opgegeven retouraanroep toohello 'verbinding' gebeurtenis is geabonneerd.
 
##### <a name="relayedconnect"></a>relayedConnect

Gewoon spiegelen Hallo `createRelayedServer` helper in de functie `relayedConnect` een clientverbinding maakt en toohello 'openen' gebeurtenis op Hallo resulterende socket is geabonneerd.

```JavaScript
var uri = WebSocket.createRelaySendUri(ns, path);
WebSocket.relayedConnect(
    uri,
    WebSocket.createRelayToken(uri, keyrule, key),
    function (socket) {
        ...
    }
);
```

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over Azure-Relay, gaat u naar deze koppelingen:
* [Wat is Azure Relay?](relay-what-is-it.md)
* [Beschikbare Relay-API 's](relay-api-overview.md)
