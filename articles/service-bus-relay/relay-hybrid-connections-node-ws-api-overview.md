---
title: Overzicht van de API van Azure Relay knooppunt | Microsoft Docs
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
ms.openlocfilehash: 28526c05c7f364f0fcaaa362fc97857f850040ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="relay-hybrid-connections-node-api-overview"></a><span data-ttu-id="6436a-103">Relay-hybride verbindingen knooppunt API-overzicht</span><span class="sxs-lookup"><span data-stu-id="6436a-103">Relay Hybrid Connections Node API overview</span></span>

## <a name="overview"></a><span data-ttu-id="6436a-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="6436a-104">Overview</span></span>

<span data-ttu-id="6436a-105">De [ `hyco-ws` ](https://www.npmjs.com/package/hyco-ws) knooppunt-pakket voor Azure Relay hybride verbindingen is gebaseerd op en breidt de ['ws'](https://www.npmjs.com/package/ws) NPM-pakket.</span><span class="sxs-lookup"><span data-stu-id="6436a-105">The [`hyco-ws`](https://www.npmjs.com/package/hyco-ws) Node package for Azure Relay Hybrid Connections is built on and extends the ['ws'](https://www.npmjs.com/package/ws) NPM package.</span></span> <span data-ttu-id="6436a-106">Dit pakket opnieuw exporteert uitvoer van dat base pakket en voegt nieuwe uitvoer die integratie met de functie Azure Relay service hybride verbindingen inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6436a-106">This package re-exports all exports of that base package and adds new exports that enable integration with the Azure Relay service Hybrid Connections feature.</span></span> 

<span data-ttu-id="6436a-107">Bestaande toepassingen die `require('ws')` kunt dit pakket met `require('hyco-ws')` in plaats daarvan ook waardoor hybride scenario's waarin een toepassing kunt luisteren voor WebSocket-verbindingen van 'binnen de firewall' lokaal en via hybride verbindingen, alles op hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="6436a-107">Existing applications that `require('ws')` can use this package with `require('hyco-ws')` instead, which also enables hybrid scenarios in which an application can listen for WebSocket connections locally from "inside the firewall" and via Hybrid Connections, all at the same time.</span></span>
  
## <a name="documentation"></a><span data-ttu-id="6436a-108">Documentatie</span><span class="sxs-lookup"><span data-stu-id="6436a-108">Documentation</span></span>

<span data-ttu-id="6436a-109">De API's zijn [gedocumenteerd in het pakket belangrijkste ws](https://github.com/websockets/ws/blob/master/doc/ws.md).</span><span class="sxs-lookup"><span data-stu-id="6436a-109">The APIs are [documented in the main 'ws' package](https://github.com/websockets/ws/blob/master/doc/ws.md).</span></span> <span data-ttu-id="6436a-110">Dit artikel wordt beschreven hoe dit pakket verschilt van die basislijn.</span><span class="sxs-lookup"><span data-stu-id="6436a-110">This article describes how this package differs from that baseline.</span></span> 

<span data-ttu-id="6436a-111">De belangrijkste verschillen tussen het basis-pakket en deze 'hyco ws' is dat het een nieuwe serverklasse, geëxporteerd toevoegt `require('hyco-ws').RelayedServer`, en een aantal methoden.</span><span class="sxs-lookup"><span data-stu-id="6436a-111">The key differences between the base package and this 'hyco-ws' is that it adds a new server class, exported via `require('hyco-ws').RelayedServer`, and a few helper methods.</span></span>

### <a name="package-helper-methods"></a><span data-ttu-id="6436a-112">Pakket Help-methoden</span><span class="sxs-lookup"><span data-stu-id="6436a-112">Package helper methods</span></span>

<span data-ttu-id="6436a-113">Er zijn verschillende hulpprogrammamethoden beschikbaar op het pakket exporteren die u kunt verwijzen naar als volgt:</span><span class="sxs-lookup"><span data-stu-id="6436a-113">There are several utility methods available on the package export that you can reference as follows:</span></span>

```JavaScript
const WebSocket = require('hyco-ws');

var listenUri = WebSocket.createRelayListenUri('namespace.servicebus.windows.net', 'path');
listenUri = WebSocket.appendRelayToken(listenUri, 'ruleName', '...key...')
...

```

<span data-ttu-id="6436a-114">De methoden voor gebruik met dit pakket zijn, maar kunnen ook worden gebruikt door de server van een knooppunt voor het inschakelen van web- of clients listeners of afzenders te maken.</span><span class="sxs-lookup"><span data-stu-id="6436a-114">The helper methods are for use with this package, but can also be used by a Node server for enabling web or device clients to create listeners or senders.</span></span> <span data-ttu-id="6436a-115">De server gebruikt deze methoden door het doorgeven van URI's waarvan de tijdelijke tokens insluiten.</span><span class="sxs-lookup"><span data-stu-id="6436a-115">The server uses these methods by passing them URIs that embed short-lived tokens.</span></span> <span data-ttu-id="6436a-116">Deze URI's kan ook worden gebruikt met algemene WebSocket-stacks die instelling HTTP-headers niet de WebSocket-handshake ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="6436a-116">These URIs can also be used with common WebSocket stacks that do not support setting HTTP headers for the WebSocket handshake.</span></span> <span data-ttu-id="6436a-117">Autorisatie tokens insluiten in de URI wordt voornamelijk voor deze bibliotheek-externe gebruiksscenario's ondersteund.</span><span class="sxs-lookup"><span data-stu-id="6436a-117">Embedding authorization tokens into the URI is supported primarily for those library-external usage scenarios.</span></span> 

#### <a name="createrelaylistenuri"></a><span data-ttu-id="6436a-118">createRelayListenUri</span><span class="sxs-lookup"><span data-stu-id="6436a-118">createRelayListenUri</span></span>

```JavaScript
var uri = createRelayListenUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="6436a-119">Maakt een geldig Azure Relay hybride verbinding listener URI voor de opgegeven naamruimte en het pad.</span><span class="sxs-lookup"><span data-stu-id="6436a-119">Creates a valid Azure Relay Hybrid Connection listener URI for the given namespace and path.</span></span> <span data-ttu-id="6436a-120">Deze URI kan vervolgens worden gebruikt met de relay-versie van de klasse WebSocketServer.</span><span class="sxs-lookup"><span data-stu-id="6436a-120">This URI can then be used with the relay version of the WebSocketServer class.</span></span>

- <span data-ttu-id="6436a-121">`namespaceName`(vereist): het domein gekwalificeerde naam van de Azure-Relay-naamruimte moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6436a-121">`namespaceName` (required) - the domain-qualified name of the Azure Relay namespace to use.</span></span>
- <span data-ttu-id="6436a-122">`path`(vereist): de naam van een bestaande hybride verbinding van een Azure-Relay in waarmee de naamruimte.</span><span class="sxs-lookup"><span data-stu-id="6436a-122">`path` (required) - the name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="6436a-123">`token`(optioneel): een eerder uitgegeven relaytoegang token die is ingesloten in de URI-listener (Zie het volgende voorbeeld).</span><span class="sxs-lookup"><span data-stu-id="6436a-123">`token` (optional) - a previously issued Relay access token that is embedded in the listener URI (see the following example).</span></span>
- <span data-ttu-id="6436a-124">`id`(optioneel): een tracerings-id end-to-end diagnostische tracering van aanvragen.</span><span class="sxs-lookup"><span data-stu-id="6436a-124">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="6436a-125">De `token` waarde is optioneel en mag alleen worden gebruikt wanneer het is niet mogelijk voor het verzenden van HTTP-headers samen met de WebSocket-handshake, zoals het geval is met de W3C-WebSocket-stack.</span><span class="sxs-lookup"><span data-stu-id="6436a-125">The `token` value is optional and should only be used when it is not possible to send HTTP headers along with the WebSocket handshake, as is the case with the W3C WebSocket stack.</span></span>                  


#### <a name="createrelaysenduri"></a><span data-ttu-id="6436a-126">createRelaySendUri</span><span class="sxs-lookup"><span data-stu-id="6436a-126">createRelaySendUri</span></span>
 
```JavaScript
var uri = createRelaySendUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="6436a-127">Hiermee maakt u een geldige Azure Relay hybride verbinding verzenden URI voor de opgegeven naamruimte en het pad.</span><span class="sxs-lookup"><span data-stu-id="6436a-127">Creates a valid Azure Relay Hybrid Connection send URI for the given namespace and path.</span></span> <span data-ttu-id="6436a-128">Deze URI kan worden gebruikt met een WebSocket-client.</span><span class="sxs-lookup"><span data-stu-id="6436a-128">This URI can be used with any WebSocket client.</span></span>

- <span data-ttu-id="6436a-129">`namespaceName`(vereist): het domein gekwalificeerde naam van de Azure-Relay-naamruimte moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6436a-129">`namespaceName` (required) - the domain-qualified name of the Azure Relay namespace to use.</span></span>
- <span data-ttu-id="6436a-130">`path`(vereist): de naam van een bestaande hybride verbinding van een Azure-Relay in waarmee de naamruimte.</span><span class="sxs-lookup"><span data-stu-id="6436a-130">`path` (required) - the name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="6436a-131">`token`(optioneel): een eerder uitgegeven relaytoegang token die is ingesloten in de URI (Zie het volgende voorbeeld).</span><span class="sxs-lookup"><span data-stu-id="6436a-131">`token` (optional) - a previously issued Relay access token that is embedded in the send URI (see the following example).</span></span>
- <span data-ttu-id="6436a-132">`id`(optioneel): een tracerings-id end-to-end diagnostische tracering van aanvragen.</span><span class="sxs-lookup"><span data-stu-id="6436a-132">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="6436a-133">De `token` waarde is optioneel en mag alleen worden gebruikt wanneer het is niet mogelijk voor het verzenden van HTTP-headers samen met de WebSocket-handshake, zoals het geval is met de W3C-WebSocket-stack.</span><span class="sxs-lookup"><span data-stu-id="6436a-133">The `token` value is optional and should only be used when it is not possible to send HTTP headers along with the WebSocket handshake, as is the case with the W3C WebSocket stack.</span></span>                   


#### <a name="createrelaytoken"></a><span data-ttu-id="6436a-134">createRelayToken</span><span class="sxs-lookup"><span data-stu-id="6436a-134">createRelayToken</span></span> 

```JavaScript
var token = createRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="6436a-135">Maakt een Azure Relay Shared Access Signature (SAS)-token voor het opgegeven doel-URI, SAS-regel en SAS-sleutel voor regel die is geldig voor het opgegeven aantal seconden of voor een uur van de huidige instant als het argument voor de verloopdatum wordt weggelaten.</span><span class="sxs-lookup"><span data-stu-id="6436a-135">Creates an Azure Relay Shared Access Signature (SAS) token for the given target URI, SAS rule, and SAS rule key that is valid for the given number of seconds or for an hour from the current instant if the expiry argument is omitted.</span></span>

- <span data-ttu-id="6436a-136">`uri`(vereist): de URI waarvan het token is worden uitgegeven.</span><span class="sxs-lookup"><span data-stu-id="6436a-136">`uri` (required) - the URI for which the token is to be issued.</span></span> <span data-ttu-id="6436a-137">De URI voor het gebruik van het HTTP-schema is genormaliseerd en querygegevens tekenreeks wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="6436a-137">The URI is normalized to use the HTTP scheme, and query string information is stripped.</span></span>
- <span data-ttu-id="6436a-138">`ruleName`(vereist) - regelnaam SAS voor beide de entiteit die wordt vertegenwoordigd door de opgegeven URI of voor de naamruimte die wordt vertegenwoordigd door het hostgedeelte van URI.</span><span class="sxs-lookup"><span data-stu-id="6436a-138">`ruleName` (required) - SAS rule name for either the entity represented by the given URI, or for the namespace represented by the URI host portion.</span></span>
- <span data-ttu-id="6436a-139">`key`(vereist) - geldige sleutel voor de SAS-regel.</span><span class="sxs-lookup"><span data-stu-id="6436a-139">`key` (required) - valid key for the SAS rule.</span></span> 
- <span data-ttu-id="6436a-140">`expirationSeconds`(optioneel): het aantal seconden totdat het gegenereerde token moet verlopen.</span><span class="sxs-lookup"><span data-stu-id="6436a-140">`expirationSeconds` (optional) - the number of seconds until the generated token should expire.</span></span> <span data-ttu-id="6436a-141">Als niet wordt opgegeven, is de standaardwaarde 1 uur (3600).</span><span class="sxs-lookup"><span data-stu-id="6436a-141">If not specified, the default is 1 hour (3600).</span></span>

<span data-ttu-id="6436a-142">Het gepubliceerde token verleent de rechten die zijn gekoppeld aan de opgegeven SAS-regel voor de opgegeven duur.</span><span class="sxs-lookup"><span data-stu-id="6436a-142">The issued token confers the rights associated with the specified SAS rule for the given duration.</span></span>

#### <a name="appendrelaytoken"></a><span data-ttu-id="6436a-143">appendRelayToken</span><span class="sxs-lookup"><span data-stu-id="6436a-143">appendRelayToken</span></span>

```JavaScript
var uri = appendRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="6436a-144">Deze methode is functioneel equivalent met de `createRelayToken` methode beschreven eerder, maar retourneert het token correct toegevoegd aan de invoer-URI.</span><span class="sxs-lookup"><span data-stu-id="6436a-144">This method is functionally equivalent to the `createRelayToken` method documented previously, but returns the token correctly appended to the input URI.</span></span>

### <a name="class-wsrelayedserver"></a><span data-ttu-id="6436a-145">Klasse ws. RelayedServer</span><span class="sxs-lookup"><span data-stu-id="6436a-145">Class ws.RelayedServer</span></span>

<span data-ttu-id="6436a-146">De `hycows.RelayedServer` klasse vormt een alternatief voor de `ws.Server` klasse die luistert niet op het lokale netwerk, maar gemachtigden luisteren naar de Azure-Relay-service.</span><span class="sxs-lookup"><span data-stu-id="6436a-146">The `hycows.RelayedServer` class is an alternative to the `ws.Server` class that does not listen on the local network, but delegates listening to the Azure Relay service.</span></span>

<span data-ttu-id="6436a-147">De twee klassen zijn voornamelijk contract die compatibel zijn, wat betekent dat een bestaande toepassing met behulp van de `ws.Server` klasse kan eenvoudig worden gewijzigd om de relayed versie te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6436a-147">The two classes are mostly contract compatible, meaning that an existing application using the `ws.Server` class can easily be changed to use the relayed version.</span></span> <span data-ttu-id="6436a-148">De belangrijkste verschillen zijn in de constructor en de beschikbare opties.</span><span class="sxs-lookup"><span data-stu-id="6436a-148">The main differences are in the constructor and in the available options.</span></span>

#### <a name="constructor"></a><span data-ttu-id="6436a-149">Constructor</span><span class="sxs-lookup"><span data-stu-id="6436a-149">Constructor</span></span>  

```JavaScript 
var ws = require('hyco-ws');
var server = ws.RelayedServer;

var wss = new server(
    {
        server: ws.createRelayListenUri(ns, path),
        token: function() { return ws.createRelayToken('http://' + ns, keyrule, key); }
    });
```

<span data-ttu-id="6436a-150">De `RelayedServer` constructor biedt ondersteuning voor een andere set argumenten dan de `Server`, omdat deze niet de listener voor een zelfstandige of kan worden ingesloten in een bestaande HTTP-listener-framework.</span><span class="sxs-lookup"><span data-stu-id="6436a-150">The `RelayedServer` constructor supports a different set of arguments than the `Server`, because it is not a standalone listener, or able to be embedded into an existing HTTP listener framework.</span></span> <span data-ttu-id="6436a-151">Er zijn ook minder mogelijkheden beschikbaar omdat de WebSocket-management grotendeels aan de Relay-service overgedragen is.</span><span class="sxs-lookup"><span data-stu-id="6436a-151">There are also fewer options available since the WebSocket management is largely delegated to the Relay service.</span></span>

<span data-ttu-id="6436a-152">Constructor-argumenten:</span><span class="sxs-lookup"><span data-stu-id="6436a-152">Constructor arguments:</span></span>

- <span data-ttu-id="6436a-153">`server`(vereist) - de volledig gekwalificeerde URI voor de naam van een hybride verbinding waarop wordt geluisterd, meestal wordt gemaakt met de WebSocket.createRelayListenUri() Help-methode.</span><span class="sxs-lookup"><span data-stu-id="6436a-153">`server` (required) - the fully qualified URI for a Hybrid Connection name on which to listen, usually constructed with the WebSocket.createRelayListenUri() helper method.</span></span>
- <span data-ttu-id="6436a-154">`token`Dit argument is (vereist) - bevat een eerder uitgegeven token tekenreeks of een callback-functie die kan worden aangeroepen voor een token tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="6436a-154">`token` (required) - this argument holds either a previously issued token string or a callback function that can be called to obtain such a token string.</span></span> <span data-ttu-id="6436a-155">De callback-optie verdient de voorkeur, zoals kunnen de vernieuwing van het token.</span><span class="sxs-lookup"><span data-stu-id="6436a-155">The callback option is preferred, as it enables token renewal.</span></span>

#### <a name="events"></a><span data-ttu-id="6436a-156">Gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="6436a-156">Events</span></span>

<span data-ttu-id="6436a-157">`RelayedServer`exemplaren verzenden drie gebeurtenissen waarmee u voor het verwerken van binnenkomende aanvragen, verbindingen tot stand brengen en foutcondities detecteren.</span><span class="sxs-lookup"><span data-stu-id="6436a-157">`RelayedServer` instances emit three events that enable you to handle incoming requests, establish connections, and detect error conditions.</span></span> <span data-ttu-id="6436a-158">U moet zich abonneren op de `connect` gebeurtenis om berichten te handelen.</span><span class="sxs-lookup"><span data-stu-id="6436a-158">You must subscribe to the `connect` event to handle messages.</span></span> 

##### <a name="headers"></a><span data-ttu-id="6436a-159">Headers</span><span class="sxs-lookup"><span data-stu-id="6436a-159">headers</span></span>

```JavaScript 
function(headers)
```

<span data-ttu-id="6436a-160">De `headers` gebeurtenis wordt geactiveerd vlak voordat een binnenkomende verbinding is geaccepteerd, het inschakelen van de wijziging van de headers worden verzonden naar de client.</span><span class="sxs-lookup"><span data-stu-id="6436a-160">The `headers` event is raised just before an incoming connection is accepted, enabling modification of the headers to send to the client.</span></span> 

##### <a name="connection"></a><span data-ttu-id="6436a-161">verbinding</span><span class="sxs-lookup"><span data-stu-id="6436a-161">connection</span></span>

```JavaScript
function(socket)
```

<span data-ttu-id="6436a-162">Verzonden wanneer een nieuwe WebSocket-verbinding is geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="6436a-162">Emitted when a new WebSocket connection is accepted.</span></span> <span data-ttu-id="6436a-163">Het object is van het type `ws.WebSocket`, net als met de basis-pakket.</span><span class="sxs-lookup"><span data-stu-id="6436a-163">The object is of type `ws.WebSocket`, same as with the base package.</span></span>


##### <a name="error"></a><span data-ttu-id="6436a-164">error</span><span class="sxs-lookup"><span data-stu-id="6436a-164">error</span></span>

```JavaScript
function(error)
```

<span data-ttu-id="6436a-165">Als de onderliggende server een fout opgetreden verzendt, is deze hier doorgestuurd.</span><span class="sxs-lookup"><span data-stu-id="6436a-165">If the underlying server emits an error, it is forwarded here.</span></span>  

#### <a name="helpers"></a><span data-ttu-id="6436a-166">Hulpprogramma 's</span><span class="sxs-lookup"><span data-stu-id="6436a-166">Helpers</span></span>

<span data-ttu-id="6436a-167">Om te beginnen een relayed server en onmiddellijk abonneren op binnenkomende verbindingen vereenvoudigen, wordt het pakket een eenvoudige Help-functie, die ook wordt gebruikt in de voorbeelden als volgt:</span><span class="sxs-lookup"><span data-stu-id="6436a-167">To simplify starting a relayed server and immediately subscribing to incoming connections, the package exposes a simple helper function, which is also used in the examples, as follows:</span></span>

##### <a name="createrelayedlistener"></a><span data-ttu-id="6436a-168">createRelayedListener</span><span class="sxs-lookup"><span data-stu-id="6436a-168">createRelayedListener</span></span>

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

##### <a name="createrelayedserver"></a><span data-ttu-id="6436a-169">createRelayedServer</span><span class="sxs-lookup"><span data-stu-id="6436a-169">createRelayedServer</span></span>

```javascript
var server = createRelayedServer([options], [connectCallback] )
```

<span data-ttu-id="6436a-170">Deze methode wordt de constructor voor het maken van een nieuw exemplaar van de RelayedServer en klik vervolgens op de opgegeven retouraanroep toe aan de gebeurtenis 'verbinding' is geabonneerd.</span><span class="sxs-lookup"><span data-stu-id="6436a-170">This method calls the constructor to create a new instance of the RelayedServer and then subscribes the provided callback to the 'connection' event.</span></span>
 
##### <a name="relayedconnect"></a><span data-ttu-id="6436a-171">relayedConnect</span><span class="sxs-lookup"><span data-stu-id="6436a-171">relayedConnect</span></span>

<span data-ttu-id="6436a-172">Spiegelen gewoon de `createRelayedServer` helper in de functie `relayedConnect` een clientverbinding maakt en de gebeurtenis 'open' op de resulterende socket is geabonneerd.</span><span class="sxs-lookup"><span data-stu-id="6436a-172">Simply mirroring the `createRelayedServer` helper in function, `relayedConnect` creates a client connection and subscribes to the 'open' event on the resulting socket.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="6436a-173">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6436a-173">Next steps</span></span>
<span data-ttu-id="6436a-174">Volg deze koppelingen voor meer informatie over Azure Relay:</span><span class="sxs-lookup"><span data-stu-id="6436a-174">To learn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="6436a-175">Wat is Azure Relay?</span><span class="sxs-lookup"><span data-stu-id="6436a-175">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="6436a-176">Beschikbare Relay-API 's</span><span class="sxs-lookup"><span data-stu-id="6436a-176">Available Relay APIs</span></span>](relay-api-overview.md)
