---
title: aaaOverview Hallo Azure Relay .NET standaard API's | Microsoft Docs
description: Relay-standaard .NET-API-overzicht
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b1da9ac1-811b-4df7-a22c-ccd013405c40
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: c90e00e809bd44eb0fbbff5eb03dfc8afa486523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a>Overzicht van Azure Relay hybride verbindingen .NET Standard API

In dit artikel ziet u een aantal van Hallo sleutel Azure Relay hybride verbindingen .NET Standard [client-API's](/dotnet/api/microsoft.azure.relay).
  
## <a name="relay-connection-string-builder"></a>Relay-verbindingsreeksen

Hallo [RelayConnectionStringBuilder] [ RelayConnectionStringBuilder] klasse indelingen verbindingsreeksen die specifieke tooRelay hybride verbindingen zijn. U kunt deze gebruiken tooverify Hallo indeling van een verbindingsreeks of toobuild een verbindingsreeks vanaf het begin. Zie Hallo code voor een voorbeeld te volgen:

```csharp
var endpoint = "{Relay namespace}";
var entityPath = "{Name of hello Hybrid Connection}";
var sharedAccessKeyName = "{SAS key name}";
var sharedAccessKey = "{SAS key value}";

var connectionStringBuilder = new RelayConnectionStringBuilder()
{
    Endpoint = endpoint,
    EntityPath = entityPath,
    SharedAccessKeyName = sasKeyName,
    SharedAccessKey = sasKeyValue
};
```

U kunt ook een verbinding doorgeven string rechtstreeks toohello `RelayConnectionStringBuilder` methode. Deze bewerking kunt u tooverify die Hallo-verbindingsreeks een ongeldige indeling is. Als een van Hallo-parameters ongeldig zijn, Hallo constructor genereert een `ArgumentException`.

```csharp
var myConnectionString = "{RelayConnectionString}";
// Declare hello connectionStringBuilder so that it can be used outside of hello loop if needed
RelayConnectionStringBuilder connectionStringBuilder;
try
{
    // Create hello connectionStringBuilder using hello supplied connection string
    connectionStringBuilder = new RelayConnectionStringBuilder(myConnectionString);
}
catch (ArgumentException ae)
{
    // Perform some error handling
}
```

## <a name="hybrid-connection-stream"></a>Stroom van hybride verbinding
Hallo [HybridConnectionStream] [ HCStream] klasse Hallo primaire object dat wordt gebruikt toosend is en gegevens ontvangen van een Azure-Relay-eindpunt, of u werkt met een [HybridConnectionClient] [ HCClient], of een [HybridConnectionListener][HCListener].

### <a name="getting-a-hybrid-connection-stream"></a>Ophalen van een Stream van hybride verbinding

#### <a name="listener"></a>Listener
Met behulp van een [HybridConnectionListener][HCListener], kunt u een `HybridConnectionStream` object als volgt:

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection toohello Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a>Client
Met behulp van een [HybridConnectionClient][HCClient], kunt u een `HybridConnectionStream` object als volgt:

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection toohello Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a>Ontvangen van gegevens
Hallo [HybridConnectionStream] [ HCStream] klasse wederzijdse communicatie mogelijk maakt. In de meeste gevallen ontvangt u continu van Hallo-stroom. Als u de tekst hello stream leest, kunt u ook toouse een [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) object, waardoor u gemakkelijker bij het parseren van Hallo-gegevens. U kunt bijvoorbeeld gegevens lezen als tekst, in plaats van als `byte[]`.

Hello volgende code weergegeven als afzonderlijke regels tekst hello stream totdat een annulering is aangevraagd:

```csharp
// Create a CancellationToken, so that we can cancel hello while loop
var cancellationToken = new CancellationToken();
// Create a StreamReader from hello 'hybridConnectionStream`
var streamReader = new StreamReader(hybridConnectionStream);

while (!cancellationToken.IsCancellationRequested)
{
    // Read a line of input until a newline is encountered
    var line = await streamReader.ReadLineAsync();
    if (string.IsNullOrEmpty(line))
    {
        // If there's no input data, we will signal that 
        // we will no longer send data on this connection
        // and then break out of hello processing loop.
        await hybridConnectionStream.ShutdownAsync(cancellationToken);
        break;
    }
}
```

### <a name="sending-data"></a>Verzenden van gegevens
Wanneer u een verbinding tot stand gebracht, kunt u een bericht toohello Relay-eindpunt te verzenden. Omdat het verbindingsobject Hallo neemt over [stroom](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), verzenden van uw gegevens als een `byte[]`. Hallo volgende voorbeeld wordt getoond hoe toodo dit:

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

Als u toosend tekst rechtstreeks wilt zonder tooencode Hallo tekenreeks telkens, kunt u echter Hallo inpakt `hybridConnectionStream` object met een [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) object.

```csharp
// hello StreamWriter object only needs toobe created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over Azure-Relay, gaat u naar deze koppelingen:

* [Microsoft.Azure.Relay verwijzing](/dotnet/api/microsoft.azure.relay)
* [Wat is Azure Relay?](relay-what-is-it.md)
* [Beschikbare Relay-API 's](relay-api-overview.md)

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener