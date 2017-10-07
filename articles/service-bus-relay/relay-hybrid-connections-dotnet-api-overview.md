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
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a><span data-ttu-id="a96a1-103">Overzicht van Azure Relay hybride verbindingen .NET Standard API</span><span class="sxs-lookup"><span data-stu-id="a96a1-103">Azure Relay Hybrid Connections .NET Standard API overview</span></span>

<span data-ttu-id="a96a1-104">In dit artikel ziet u een aantal van Hallo sleutel Azure Relay hybride verbindingen .NET Standard [client-API's](/dotnet/api/microsoft.azure.relay).</span><span class="sxs-lookup"><span data-stu-id="a96a1-104">This article summarizes some of hello key Azure Relay Hybrid Connections .NET Standard [client APIs](/dotnet/api/microsoft.azure.relay).</span></span>
  
## <a name="relay-connection-string-builder"></a><span data-ttu-id="a96a1-105">Relay-verbindingsreeksen</span><span class="sxs-lookup"><span data-stu-id="a96a1-105">Relay Connection String Builder</span></span>

<span data-ttu-id="a96a1-106">Hallo [RelayConnectionStringBuilder] [ RelayConnectionStringBuilder] klasse indelingen verbindingsreeksen die specifieke tooRelay hybride verbindingen zijn.</span><span class="sxs-lookup"><span data-stu-id="a96a1-106">hello [RelayConnectionStringBuilder][RelayConnectionStringBuilder] class formats connection strings that are specific tooRelay Hybrid Connections.</span></span> <span data-ttu-id="a96a1-107">U kunt deze gebruiken tooverify Hallo indeling van een verbindingsreeks of toobuild een verbindingsreeks vanaf het begin.</span><span class="sxs-lookup"><span data-stu-id="a96a1-107">You can use it tooverify hello format of a connection string, or toobuild a connection string from scratch.</span></span> <span data-ttu-id="a96a1-108">Zie Hallo code voor een voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="a96a1-108">See hello following code for an example:</span></span>

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

<span data-ttu-id="a96a1-109">U kunt ook een verbinding doorgeven string rechtstreeks toohello `RelayConnectionStringBuilder` methode.</span><span class="sxs-lookup"><span data-stu-id="a96a1-109">You can also pass a connection string directly toohello `RelayConnectionStringBuilder` method.</span></span> <span data-ttu-id="a96a1-110">Deze bewerking kunt u tooverify die Hallo-verbindingsreeks een ongeldige indeling is.</span><span class="sxs-lookup"><span data-stu-id="a96a1-110">This operation enables you tooverify that hello connection string is in a valid format.</span></span> <span data-ttu-id="a96a1-111">Als een van Hallo-parameters ongeldig zijn, Hallo constructor genereert een `ArgumentException`.</span><span class="sxs-lookup"><span data-stu-id="a96a1-111">If any of hello parameters are invalid, hello constructor generates an `ArgumentException`.</span></span>

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

## <a name="hybrid-connection-stream"></a><span data-ttu-id="a96a1-112">Stroom van hybride verbinding</span><span class="sxs-lookup"><span data-stu-id="a96a1-112">Hybrid Connection Stream</span></span>
<span data-ttu-id="a96a1-113">Hallo [HybridConnectionStream] [ HCStream] klasse Hallo primaire object dat wordt gebruikt toosend is en gegevens ontvangen van een Azure-Relay-eindpunt, of u werkt met een [HybridConnectionClient] [ HCClient], of een [HybridConnectionListener][HCListener].</span><span class="sxs-lookup"><span data-stu-id="a96a1-113">hello [HybridConnectionStream][HCStream] class is hello primary object used toosend and receive data from an Azure Relay endpoint, whether you are working with a [HybridConnectionClient][HCClient], or a [HybridConnectionListener][HCListener].</span></span>

### <a name="getting-a-hybrid-connection-stream"></a><span data-ttu-id="a96a1-114">Ophalen van een Stream van hybride verbinding</span><span class="sxs-lookup"><span data-stu-id="a96a1-114">Getting a Hybrid Connection Stream</span></span>

#### <a name="listener"></a><span data-ttu-id="a96a1-115">Listener</span><span class="sxs-lookup"><span data-stu-id="a96a1-115">Listener</span></span>
<span data-ttu-id="a96a1-116">Met behulp van een [HybridConnectionListener][HCListener], kunt u een `HybridConnectionStream` object als volgt:</span><span class="sxs-lookup"><span data-stu-id="a96a1-116">Using a [HybridConnectionListener][HCListener], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection toohello Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a><span data-ttu-id="a96a1-117">Client</span><span class="sxs-lookup"><span data-stu-id="a96a1-117">Client</span></span>
<span data-ttu-id="a96a1-118">Met behulp van een [HybridConnectionClient][HCClient], kunt u een `HybridConnectionStream` object als volgt:</span><span class="sxs-lookup"><span data-stu-id="a96a1-118">Using a [HybridConnectionClient][HCClient], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection toohello Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a><span data-ttu-id="a96a1-119">Ontvangen van gegevens</span><span class="sxs-lookup"><span data-stu-id="a96a1-119">Receiving data</span></span>
<span data-ttu-id="a96a1-120">Hallo [HybridConnectionStream] [ HCStream] klasse wederzijdse communicatie mogelijk maakt.</span><span class="sxs-lookup"><span data-stu-id="a96a1-120">hello [HybridConnectionStream][HCStream] class enables two-way communication.</span></span> <span data-ttu-id="a96a1-121">In de meeste gevallen ontvangt u continu van Hallo-stroom.</span><span class="sxs-lookup"><span data-stu-id="a96a1-121">In most cases, you continuously receive from hello stream.</span></span> <span data-ttu-id="a96a1-122">Als u de tekst hello stream leest, kunt u ook toouse een [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) object, waardoor u gemakkelijker bij het parseren van Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="a96a1-122">If you are reading text from hello stream, you may also want toouse a [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) object, which enables easier parsing of hello data.</span></span> <span data-ttu-id="a96a1-123">U kunt bijvoorbeeld gegevens lezen als tekst, in plaats van als `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="a96a1-123">For example, you can read data as text, rather than as `byte[]`.</span></span>

<span data-ttu-id="a96a1-124">Hello volgende code weergegeven als afzonderlijke regels tekst hello stream totdat een annulering is aangevraagd:</span><span class="sxs-lookup"><span data-stu-id="a96a1-124">hello following code reads individual lines of text from hello stream until a cancellation is requested:</span></span>

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

### <a name="sending-data"></a><span data-ttu-id="a96a1-125">Verzenden van gegevens</span><span class="sxs-lookup"><span data-stu-id="a96a1-125">Sending data</span></span>
<span data-ttu-id="a96a1-126">Wanneer u een verbinding tot stand gebracht, kunt u een bericht toohello Relay-eindpunt te verzenden.</span><span class="sxs-lookup"><span data-stu-id="a96a1-126">Once you have a connection established, you can send a message toohello Relay endpoint.</span></span> <span data-ttu-id="a96a1-127">Omdat het verbindingsobject Hallo neemt over [stroom](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), verzenden van uw gegevens als een `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="a96a1-127">Because hello connection object inherits [Stream](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), send your data as a `byte[]`.</span></span> <span data-ttu-id="a96a1-128">Hallo volgende voorbeeld wordt getoond hoe toodo dit:</span><span class="sxs-lookup"><span data-stu-id="a96a1-128">hello following example shows how toodo this:</span></span>

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

<span data-ttu-id="a96a1-129">Als u toosend tekst rechtstreeks wilt zonder tooencode Hallo tekenreeks telkens, kunt u echter Hallo inpakt `hybridConnectionStream` object met een [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) object.</span><span class="sxs-lookup"><span data-stu-id="a96a1-129">However, if you want toosend text directly, without needing tooencode hello string each time, you can wrap hello `hybridConnectionStream` object with a [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) object.</span></span>

```csharp
// hello StreamWriter object only needs toobe created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a><span data-ttu-id="a96a1-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a96a1-130">Next steps</span></span>
<span data-ttu-id="a96a1-131">toolearn meer informatie over Azure-Relay, gaat u naar deze koppelingen:</span><span class="sxs-lookup"><span data-stu-id="a96a1-131">toolearn more about Azure Relay, visit these links:</span></span>

* [<span data-ttu-id="a96a1-132">Microsoft.Azure.Relay verwijzing</span><span class="sxs-lookup"><span data-stu-id="a96a1-132">Microsoft.Azure.Relay reference</span></span>](/dotnet/api/microsoft.azure.relay)
* [<span data-ttu-id="a96a1-133">Wat is Azure Relay?</span><span class="sxs-lookup"><span data-stu-id="a96a1-133">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="a96a1-134">Beschikbare Relay-API 's</span><span class="sxs-lookup"><span data-stu-id="a96a1-134">Available Relay APIs</span></span>](relay-api-overview.md)

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener