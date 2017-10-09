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
# <a name="relay-hybrid-connections-node-api-overview"></a><span data-ttu-id="b2c5d-103">Relay-hybride verbindingen knooppunt API-overzicht</span><span class="sxs-lookup"><span data-stu-id="b2c5d-103">Relay Hybrid Connections Node API overview</span></span>

## <a name="overview"></a><span data-ttu-id="b2c5d-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="b2c5d-104">Overview</span></span>

<span data-ttu-id="b2c5d-105">Hallo [ `hyco-ws` ](https://www.npmjs.com/package/hyco-ws) knooppunt-pakket voor Azure Relay hybride verbindingen is gebaseerd op en breidt Hallo ['ws'](https://www.npmjs.com/package/ws) NPM-pakket.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-105">hello [`hyco-ws`](https://www.npmjs.com/package/hyco-ws) Node package for Azure Relay Hybrid Connections is built on and extends hello ['ws'](https://www.npmjs.com/package/ws) NPM package.</span></span> <span data-ttu-id="b2c5d-106">Dit pakket opnieuw exporteert uitvoer van dat base pakket en voegt nieuwe uitvoer die integratie met de functie hybride verbindingen hello Azure Relay-service inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-106">This package re-exports all exports of that base package and adds new exports that enable integration with hello Azure Relay service Hybrid Connections feature.</span></span> 

<span data-ttu-id="b2c5d-107">Bestaande toepassingen die `require('ws')` kunt dit pakket met `require('hyco-ws')` in plaats daarvan ook waardoor hybride scenario's waarin een toepassing kunt luisteren voor WebSocket-verbindingen lokaal uit 'binnen de firewall Hallo' en via de hybride verbindingen, alles op Hallo dezelfde tijd.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-107">Existing applications that `require('ws')` can use this package with `require('hyco-ws')` instead, which also enables hybrid scenarios in which an application can listen for WebSocket connections locally from "inside hello firewall" and via Hybrid Connections, all at hello same time.</span></span>
  
## <a name="documentation"></a><span data-ttu-id="b2c5d-108">Documentatie</span><span class="sxs-lookup"><span data-stu-id="b2c5d-108">Documentation</span></span>

<span data-ttu-id="b2c5d-109">Hallo-API's zijn [gedocumenteerd in Hallo belangrijkste ws pakket](https://github.com/websockets/ws/blob/master/doc/ws.md).</span><span class="sxs-lookup"><span data-stu-id="b2c5d-109">hello APIs are [documented in hello main 'ws' package](https://github.com/websockets/ws/blob/master/doc/ws.md).</span></span> <span data-ttu-id="b2c5d-110">Dit artikel wordt beschreven hoe dit pakket verschilt van die basislijn.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-110">This article describes how this package differs from that baseline.</span></span> 

<span data-ttu-id="b2c5d-111">Hallo belangrijke verschillen tussen Hallo base pakket en deze 'hyco ws' is dat het een nieuwe serverklasse, geëxporteerd toevoegt `require('hyco-ws').RelayedServer`, en een aantal methoden.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-111">hello key differences between hello base package and this 'hyco-ws' is that it adds a new server class, exported via `require('hyco-ws').RelayedServer`, and a few helper methods.</span></span>

### <a name="package-helper-methods"></a><span data-ttu-id="b2c5d-112">Pakket Help-methoden</span><span class="sxs-lookup"><span data-stu-id="b2c5d-112">Package helper methods</span></span>

<span data-ttu-id="b2c5d-113">Er zijn verschillende hulpprogrammamethoden beschikbaar op Hallo pakket exporteren die u kunt verwijzen naar als volgt:</span><span class="sxs-lookup"><span data-stu-id="b2c5d-113">There are several utility methods available on hello package export that you can reference as follows:</span></span>

```JavaScript
const WebSocket = require('hyco-ws');

var listenUri = WebSocket.createRelayListenUri('namespace.servicebus.windows.net', 'path');
listenUri = WebSocket.appendRelayToken(listenUri, 'ruleName', '...key...')
...

```

<span data-ttu-id="b2c5d-114">Hallo helpmethoden zijn voor gebruik met dit pakket, maar kunnen ook worden gebruikt door de server van een knooppunt voor het inschakelen van web- of clients toocreate listeners of afzenders.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-114">hello helper methods are for use with this package, but can also be used by a Node server for enabling web or device clients toocreate listeners or senders.</span></span> <span data-ttu-id="b2c5d-115">Hallo-server gebruikt deze methoden door het doorgeven van URI's waarvan de tijdelijke tokens insluiten.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-115">hello server uses these methods by passing them URIs that embed short-lived tokens.</span></span> <span data-ttu-id="b2c5d-116">Deze URI's kan ook worden gebruikt met algemene WebSocket-stacks die instelling HTTP-headers niet Hallo WebSocket-handshake ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-116">These URIs can also be used with common WebSocket stacks that do not support setting HTTP headers for hello WebSocket handshake.</span></span> <span data-ttu-id="b2c5d-117">Autorisatie tokens insluiten in Hallo die URI hoofdzakelijk voor deze bibliotheek-externe gebruiksscenario's wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-117">Embedding authorization tokens into hello URI is supported primarily for those library-external usage scenarios.</span></span> 

#### <a name="createrelaylistenuri"></a><span data-ttu-id="b2c5d-118">createRelayListenUri</span><span class="sxs-lookup"><span data-stu-id="b2c5d-118">createRelayListenUri</span></span>

```JavaScript
var uri = createRelayListenUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="b2c5d-119">Maakt een geldig Azure Relay hybride verbinding listener URI voor Hallo opgegeven naamruimte en het pad.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-119">Creates a valid Azure Relay Hybrid Connection listener URI for hello given namespace and path.</span></span> <span data-ttu-id="b2c5d-120">Deze URI kan vervolgens worden gebruikt met Hallo relay-versie van Hallo WebSocketServer klasse.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-120">This URI can then be used with hello relay version of hello WebSocketServer class.</span></span>

- <span data-ttu-id="b2c5d-121">`namespaceName`(vereist) - domein gekwalificeerde naam van hello Azure Relay naamruimte toouse Hallo.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-121">`namespaceName` (required) - hello domain-qualified name of hello Azure Relay namespace toouse.</span></span>
- <span data-ttu-id="b2c5d-122">`path`(vereist) - naam van een bestaande hybride verbinding van een Azure-Relay in die naamruimte Hallo.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-122">`path` (required) - hello name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="b2c5d-123">`token`(optioneel): een eerder uitgegeven relaytoegang token die is ingesloten in Hallo listener URI (Zie het volgende voorbeeld Hallo).</span><span class="sxs-lookup"><span data-stu-id="b2c5d-123">`token` (optional) - a previously issued Relay access token that is embedded in hello listener URI (see hello following example).</span></span>
- <span data-ttu-id="b2c5d-124">`id`(optioneel): een tracerings-id end-to-end diagnostische tracering van aanvragen.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-124">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="b2c5d-125">Hallo `token` waarde is optioneel en mag alleen worden gebruikt wanneer het niet mogelijk toosend HTTP-headers samen met de WebSocket-handshake hello, zoals Hallo geval met Hallo W3C WebSocket-stack.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-125">hello `token` value is optional and should only be used when it is not possible toosend HTTP headers along with hello WebSocket handshake, as is hello case with hello W3C WebSocket stack.</span></span>                  


#### <a name="createrelaysenduri"></a><span data-ttu-id="b2c5d-126">createRelaySendUri</span><span class="sxs-lookup"><span data-stu-id="b2c5d-126">createRelaySendUri</span></span>
 
```JavaScript
var uri = createRelaySendUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="b2c5d-127">Hiermee maakt u een geldige Azure Relay hybride verbinding verzenden URI voor Hallo opgegeven naamruimte en het pad.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-127">Creates a valid Azure Relay Hybrid Connection send URI for hello given namespace and path.</span></span> <span data-ttu-id="b2c5d-128">Deze URI kan worden gebruikt met een WebSocket-client.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-128">This URI can be used with any WebSocket client.</span></span>

- <span data-ttu-id="b2c5d-129">`namespaceName`(vereist) - domein gekwalificeerde naam van hello Azure Relay naamruimte toouse Hallo.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-129">`namespaceName` (required) - hello domain-qualified name of hello Azure Relay namespace toouse.</span></span>
- <span data-ttu-id="b2c5d-130">`path`(vereist) - naam van een bestaande hybride verbinding van een Azure-Relay in die naamruimte Hallo.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-130">`path` (required) - hello name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="b2c5d-131">`token`(optioneel): een eerder uitgegeven Relay toegangstoken dat is ingesloten in Hallo URI verzenden (Zie het volgende voorbeeld Hallo).</span><span class="sxs-lookup"><span data-stu-id="b2c5d-131">`token` (optional) - a previously issued Relay access token that is embedded in hello send URI (see hello following example).</span></span>
- <span data-ttu-id="b2c5d-132">`id`(optioneel): een tracerings-id end-to-end diagnostische tracering van aanvragen.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-132">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="b2c5d-133">Hallo `token` waarde is optioneel en mag alleen worden gebruikt wanneer het niet mogelijk toosend HTTP-headers samen met de WebSocket-handshake hello, zoals Hallo geval met Hallo W3C WebSocket-stack.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-133">hello `token` value is optional and should only be used when it is not possible toosend HTTP headers along with hello WebSocket handshake, as is hello case with hello W3C WebSocket stack.</span></span>                   


#### <a name="createrelaytoken"></a><span data-ttu-id="b2c5d-134">createRelayToken</span><span class="sxs-lookup"><span data-stu-id="b2c5d-134">createRelayToken</span></span> 

```JavaScript
var token = createRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="b2c5d-135">Hiermee maakt u een Azure Relay Shared Access Signature (SAS)-token voor Hallo opgegeven doel-URI, SAS-regel en SAS-sleutel voor regel die geldig is voor Hallo aantal seconden of een uur wordt gegeven van de huidige Hallo instant als Hallo verstrijken argument wordt weggelaten.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-135">Creates an Azure Relay Shared Access Signature (SAS) token for hello given target URI, SAS rule, and SAS rule key that is valid for hello given number of seconds or for an hour from hello current instant if hello expiry argument is omitted.</span></span>

- <span data-ttu-id="b2c5d-136">`uri`(vereist) - URI voor welke Hallo-token uitgegeven toobe is Hallo.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-136">`uri` (required) - hello URI for which hello token is toobe issued.</span></span> <span data-ttu-id="b2c5d-137">Hallo-URI is genormaliseerde toouse Hallo HTTP-schema en querygegevens tekenreeks wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-137">hello URI is normalized toouse hello HTTP scheme, and query string information is stripped.</span></span>
- <span data-ttu-id="b2c5d-138">`ruleName`(vereist) - SAS-Regelnaam voor beide dat wordt vertegenwoordigd door de opgegeven URI Hallo Hallo-entiteit of voor Hallo naamruimte dat wordt vertegenwoordigd door Hallo hostgedeelte URI.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-138">`ruleName` (required) - SAS rule name for either hello entity represented by hello given URI, or for hello namespace represented by hello URI host portion.</span></span>
- <span data-ttu-id="b2c5d-139">`key`(vereist) - geldige sleutel voor Hallo SAS-regel.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-139">`key` (required) - valid key for hello SAS rule.</span></span> 
- <span data-ttu-id="b2c5d-140">`expirationSeconds`(optioneel): het aantal seconden totdat Hallo gegenereerd token Hallo moet verlopen.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-140">`expirationSeconds` (optional) - hello number of seconds until hello generated token should expire.</span></span> <span data-ttu-id="b2c5d-141">Als niet wordt opgegeven, is standaard Hallo 1 uur (3600).</span><span class="sxs-lookup"><span data-stu-id="b2c5d-141">If not specified, hello default is 1 hour (3600).</span></span>

<span data-ttu-id="b2c5d-142">Hallo uitgegeven token verleent Hallo rechten die zijn gekoppeld aan Hallo opgegeven SAS-regel voor Hallo opgegeven duur.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-142">hello issued token confers hello rights associated with hello specified SAS rule for hello given duration.</span></span>

#### <a name="appendrelaytoken"></a><span data-ttu-id="b2c5d-143">appendRelayToken</span><span class="sxs-lookup"><span data-stu-id="b2c5d-143">appendRelayToken</span></span>

```JavaScript
var uri = appendRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="b2c5d-144">Deze methode is functioneel equivalent toohello `createRelayToken` methode eerder beschreven, maar retourneert Hallo token correct toegevoegde toohello invoer-URI.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-144">This method is functionally equivalent toohello `createRelayToken` method documented previously, but returns hello token correctly appended toohello input URI.</span></span>

### <a name="class-wsrelayedserver"></a><span data-ttu-id="b2c5d-145">Klasse ws. RelayedServer</span><span class="sxs-lookup"><span data-stu-id="b2c5d-145">Class ws.RelayedServer</span></span>

<span data-ttu-id="b2c5d-146">Hallo `hycows.RelayedServer` klasse is een alternatieve toohello `ws.Server` klasse die luistert niet op het lokale netwerk hello, maar delegeert luisterende toohello Azure Relay-service.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-146">hello `hycows.RelayedServer` class is an alternative toohello `ws.Server` class that does not listen on hello local network, but delegates listening toohello Azure Relay service.</span></span>

<span data-ttu-id="b2c5d-147">Hallo twee klassen zijn voornamelijk contract die compatibel zijn, wat betekent dat een bestaande toepassing hello met `ws.Server` klasse kan eenvoudig worden gewijzigd toouse Hallo relayed versie.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-147">hello two classes are mostly contract compatible, meaning that an existing application using hello `ws.Server` class can easily be changed toouse hello relayed version.</span></span> <span data-ttu-id="b2c5d-148">de belangrijkste verschillen Hallo zijn in de constructor Hallo en Hallo beschikbare opties.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-148">hello main differences are in hello constructor and in hello available options.</span></span>

#### <a name="constructor"></a><span data-ttu-id="b2c5d-149">Constructor</span><span class="sxs-lookup"><span data-stu-id="b2c5d-149">Constructor</span></span>  

```JavaScript 
var ws = require('hyco-ws');
var server = ws.RelayedServer;

var wss = new server(
    {
        server: ws.createRelayListenUri(ns, path),
        token: function() { return ws.createRelayToken('http://' + ns, keyrule, key); }
    });
```

<span data-ttu-id="b2c5d-150">Hallo `RelayedServer` constructor biedt ondersteuning voor een andere set argumenten dan Hallo `Server`, omdat het is niet een zelfstandige listener of kunnen toobe ingesloten in een bestaande HTTP-listener-framework.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-150">hello `RelayedServer` constructor supports a different set of arguments than hello `Server`, because it is not a standalone listener, or able toobe embedded into an existing HTTP listener framework.</span></span> <span data-ttu-id="b2c5d-151">Er zijn ook minder mogelijkheden beschikbaar aangezien Hallo WebSocket management grotendeels gedelegeerd toohello Relay-service.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-151">There are also fewer options available since hello WebSocket management is largely delegated toohello Relay service.</span></span>

<span data-ttu-id="b2c5d-152">Constructor-argumenten:</span><span class="sxs-lookup"><span data-stu-id="b2c5d-152">Constructor arguments:</span></span>

- <span data-ttu-id="b2c5d-153">`server`(vereist) - gekwalificeerde Hallo volledig URI voor de naam van een hybride verbinding op welke toolisten, meestal met Hallo WebSocket.createRelayListenUri() Help-methode wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-153">`server` (required) - hello fully qualified URI for a Hybrid Connection name on which toolisten, usually constructed with hello WebSocket.createRelayListenUri() helper method.</span></span>
- <span data-ttu-id="b2c5d-154">`token`Dit argument is (vereist) - bevat een eerder uitgegeven token tekenreeks of een callback-functie die een token tekenreeks tooobtain kan worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-154">`token` (required) - this argument holds either a previously issued token string or a callback function that can be called tooobtain such a token string.</span></span> <span data-ttu-id="b2c5d-155">Hallo callback optie verdient de voorkeur, zoals kunnen de vernieuwing van het token.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-155">hello callback option is preferred, as it enables token renewal.</span></span>

#### <a name="events"></a><span data-ttu-id="b2c5d-156">Gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="b2c5d-156">Events</span></span>

<span data-ttu-id="b2c5d-157">`RelayedServer`exemplaren verzenden drie gebeurtenissen die u toohandle binnenkomende aanvragen inschakelen, verbindingen tot stand brengen en foutcondities detecteren.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-157">`RelayedServer` instances emit three events that enable you toohandle incoming requests, establish connections, and detect error conditions.</span></span> <span data-ttu-id="b2c5d-158">U moet zich abonneren toohello `connect` toohandle gebeurtenisberichten.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-158">You must subscribe toohello `connect` event toohandle messages.</span></span> 

##### <a name="headers"></a><span data-ttu-id="b2c5d-159">Headers</span><span class="sxs-lookup"><span data-stu-id="b2c5d-159">headers</span></span>

```JavaScript 
function(headers)
```

<span data-ttu-id="b2c5d-160">Hallo `headers` gebeurtenis wordt geactiveerd vlak voordat een binnenkomende verbinding is geaccepteerd, wijziging van Hallo headers toosend toohello client inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-160">hello `headers` event is raised just before an incoming connection is accepted, enabling modification of hello headers toosend toohello client.</span></span> 

##### <a name="connection"></a><span data-ttu-id="b2c5d-161">verbinding</span><span class="sxs-lookup"><span data-stu-id="b2c5d-161">connection</span></span>

```JavaScript
function(socket)
```

<span data-ttu-id="b2c5d-162">Verzonden wanneer een nieuwe WebSocket-verbinding is geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-162">Emitted when a new WebSocket connection is accepted.</span></span> <span data-ttu-id="b2c5d-163">Hallo-object is van het type `ws.WebSocket`, net als met base Hallo-pakket.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-163">hello object is of type `ws.WebSocket`, same as with hello base package.</span></span>


##### <a name="error"></a><span data-ttu-id="b2c5d-164">error</span><span class="sxs-lookup"><span data-stu-id="b2c5d-164">error</span></span>

```JavaScript
function(error)
```

<span data-ttu-id="b2c5d-165">Als de onderliggende Hallo-server verzendt een fout opgetreden, is deze hier doorgestuurd.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-165">If hello underlying server emits an error, it is forwarded here.</span></span>  

#### <a name="helpers"></a><span data-ttu-id="b2c5d-166">Hulpprogramma 's</span><span class="sxs-lookup"><span data-stu-id="b2c5d-166">Helpers</span></span>

<span data-ttu-id="b2c5d-167">toosimplify vanaf een relayed server en onmiddellijk abonneren tooincoming verbindingen, Hallo van het pakket wordt een eenvoudige Help-functie, die ook wordt gebruikt in de voorbeelden hello, als volgt:</span><span class="sxs-lookup"><span data-stu-id="b2c5d-167">toosimplify starting a relayed server and immediately subscribing tooincoming connections, hello package exposes a simple helper function, which is also used in hello examples, as follows:</span></span>

##### <a name="createrelayedlistener"></a><span data-ttu-id="b2c5d-168">createRelayedListener</span><span class="sxs-lookup"><span data-stu-id="b2c5d-168">createRelayedListener</span></span>

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

##### <a name="createrelayedserver"></a><span data-ttu-id="b2c5d-169">createRelayedServer</span><span class="sxs-lookup"><span data-stu-id="b2c5d-169">createRelayedServer</span></span>

```javascript
var server = createRelayedServer([options], [connectCallback] )
```

<span data-ttu-id="b2c5d-170">Deze methode aanroept Hallo constructor toocreate een nieuw exemplaar van Hallo RelayedServer en vervolgens Hallo opgegeven retouraanroep toohello 'verbinding' gebeurtenis is geabonneerd.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-170">This method calls hello constructor toocreate a new instance of hello RelayedServer and then subscribes hello provided callback toohello 'connection' event.</span></span>
 
##### <a name="relayedconnect"></a><span data-ttu-id="b2c5d-171">relayedConnect</span><span class="sxs-lookup"><span data-stu-id="b2c5d-171">relayedConnect</span></span>

<span data-ttu-id="b2c5d-172">Gewoon spiegelen Hallo `createRelayedServer` helper in de functie `relayedConnect` een clientverbinding maakt en toohello 'openen' gebeurtenis op Hallo resulterende socket is geabonneerd.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-172">Simply mirroring hello `createRelayedServer` helper in function, `relayedConnect` creates a client connection and subscribes toohello 'open' event on hello resulting socket.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b2c5d-173">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b2c5d-173">Next steps</span></span>
<span data-ttu-id="b2c5d-174">toolearn meer informatie over Azure-Relay, gaat u naar deze koppelingen:</span><span class="sxs-lookup"><span data-stu-id="b2c5d-174">toolearn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="b2c5d-175">Wat is Azure Relay?</span><span class="sxs-lookup"><span data-stu-id="b2c5d-175">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="b2c5d-176">Beschikbare Relay-API 's</span><span class="sxs-lookup"><span data-stu-id="b2c5d-176">Available Relay APIs</span></span>](relay-api-overview.md)
