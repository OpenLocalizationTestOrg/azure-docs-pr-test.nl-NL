---
title: Overzicht van de Azure Relay standaard .NET API's | Microsoft Docs
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
ms.openlocfilehash: f3f4a2e721b1a75a5b92a5c17a9939c7013340d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a><span data-ttu-id="e895a-103">Overzicht van Azure Relay hybride verbindingen .NET Standard API</span><span class="sxs-lookup"><span data-stu-id="e895a-103">Azure Relay Hybrid Connections .NET Standard API overview</span></span>

<span data-ttu-id="e895a-104">In dit artikel ziet u een aantal van de sleutel Azure Relay hybride verbindingen .NET Standard [client-API's](/dotnet/api/microsoft.azure.relay).</span><span class="sxs-lookup"><span data-stu-id="e895a-104">This article summarizes some of the key Azure Relay Hybrid Connections .NET Standard [client APIs](/dotnet/api/microsoft.azure.relay).</span></span>
  
## <a name="relay-connection-string-builder"></a><span data-ttu-id="e895a-105">Relay-verbindingsreeksen</span><span class="sxs-lookup"><span data-stu-id="e895a-105">Relay Connection String Builder</span></span>

<span data-ttu-id="e895a-106">De [RelayConnectionStringBuilder] [ RelayConnectionStringBuilder] klasse indelingen verbindingsreeksen die specifiek voor Relay hybride verbindingen zijn.</span><span class="sxs-lookup"><span data-stu-id="e895a-106">The [RelayConnectionStringBuilder][RelayConnectionStringBuilder] class formats connection strings that are specific to Relay Hybrid Connections.</span></span> <span data-ttu-id="e895a-107">U kunt deze gebruiken om te controleren of de indeling van een verbindingsreeks of een verbindingsreeks vanaf het begin.</span><span class="sxs-lookup"><span data-stu-id="e895a-107">You can use it to verify the format of a connection string, or to build a connection string from scratch.</span></span> <span data-ttu-id="e895a-108">Zie de volgende code voor een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e895a-108">See the following code for an example:</span></span>

```csharp
var endpoint = "{Relay namespace}";
var entityPath = "{Name of the Hybrid Connection}";
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

<span data-ttu-id="e895a-109">U kunt ook een verbindingsreeks rechtstreeks naar doorgeven de `RelayConnectionStringBuilder` methode.</span><span class="sxs-lookup"><span data-stu-id="e895a-109">You can also pass a connection string directly to the `RelayConnectionStringBuilder` method.</span></span> <span data-ttu-id="e895a-110">Deze bewerking kunt u controleren of de verbindingsreeks is een ongeldige indeling.</span><span class="sxs-lookup"><span data-stu-id="e895a-110">This operation enables you to verify that the connection string is in a valid format.</span></span> <span data-ttu-id="e895a-111">Als u een van de parameters zijn ongeldig, de constructor genereert een `ArgumentException`.</span><span class="sxs-lookup"><span data-stu-id="e895a-111">If any of the parameters are invalid, the constructor generates an `ArgumentException`.</span></span>

```csharp
var myConnectionString = "{RelayConnectionString}";
// Declare the connectionStringBuilder so that it can be used outside of the loop if needed
RelayConnectionStringBuilder connectionStringBuilder;
try
{
    // Create the connectionStringBuilder using the supplied connection string
    connectionStringBuilder = new RelayConnectionStringBuilder(myConnectionString);
}
catch (ArgumentException ae)
{
    // Perform some error handling
}
```

## <a name="hybrid-connection-stream"></a><span data-ttu-id="e895a-112">Stroom van hybride verbinding</span><span class="sxs-lookup"><span data-stu-id="e895a-112">Hybrid Connection Stream</span></span>
<span data-ttu-id="e895a-113">De [HybridConnectionStream] [ HCStream] klasse is de primaire object dat wordt gebruikt voor het verzenden en ontvangen van gegevens van een eindpunt Azure Relay of u met werkt een [HybridConnectionClient] [ HCClient], of een [HybridConnectionListener][HCListener].</span><span class="sxs-lookup"><span data-stu-id="e895a-113">The [HybridConnectionStream][HCStream] class is the primary object used to send and receive data from an Azure Relay endpoint, whether you are working with a [HybridConnectionClient][HCClient], or a [HybridConnectionListener][HCListener].</span></span>

### <a name="getting-a-hybrid-connection-stream"></a><span data-ttu-id="e895a-114">Ophalen van een Stream van hybride verbinding</span><span class="sxs-lookup"><span data-stu-id="e895a-114">Getting a Hybrid Connection Stream</span></span>

#### <a name="listener"></a><span data-ttu-id="e895a-115">Listener</span><span class="sxs-lookup"><span data-stu-id="e895a-115">Listener</span></span>
<span data-ttu-id="e895a-116">Met behulp van een [HybridConnectionListener][HCListener], kunt u een `HybridConnectionStream` object als volgt:</span><span class="sxs-lookup"><span data-stu-id="e895a-116">Using a [HybridConnectionListener][HCListener], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use the RelayConnectionStringBuilder to get a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection to the Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a><span data-ttu-id="e895a-117">Client</span><span class="sxs-lookup"><span data-stu-id="e895a-117">Client</span></span>
<span data-ttu-id="e895a-118">Met behulp van een [HybridConnectionClient][HCClient], kunt u een `HybridConnectionStream` object als volgt:</span><span class="sxs-lookup"><span data-stu-id="e895a-118">Using a [HybridConnectionClient][HCClient], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use the RelayConnectionStringBuilder to get a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection to the Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a><span data-ttu-id="e895a-119">Ontvangen van gegevens</span><span class="sxs-lookup"><span data-stu-id="e895a-119">Receiving data</span></span>
<span data-ttu-id="e895a-120">De [HybridConnectionStream] [ HCStream] klasse wederzijdse communicatie mogelijk maakt.</span><span class="sxs-lookup"><span data-stu-id="e895a-120">The [HybridConnectionStream][HCStream] class enables two-way communication.</span></span> <span data-ttu-id="e895a-121">In de meeste gevallen ontvangt u continu van de stroom.</span><span class="sxs-lookup"><span data-stu-id="e895a-121">In most cases, you continuously receive from the stream.</span></span> <span data-ttu-id="e895a-122">Als u tekst uit de stroom leest, u kunt ook gebruik van een [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) object, waardoor u gemakkelijker bij het parseren van de gegevens.</span><span class="sxs-lookup"><span data-stu-id="e895a-122">If you are reading text from the stream, you may also want to use a [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) object, which enables easier parsing of the data.</span></span> <span data-ttu-id="e895a-123">U kunt bijvoorbeeld gegevens lezen als tekst, in plaats van als `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="e895a-123">For example, you can read data as text, rather than as `byte[]`.</span></span>

<span data-ttu-id="e895a-124">De volgende code worden afzonderlijke tekstregels gelezen uit de stroom totdat een annulering is aangevraagd:</span><span class="sxs-lookup"><span data-stu-id="e895a-124">The following code reads individual lines of text from the stream until a cancellation is requested:</span></span>

```csharp
// Create a CancellationToken, so that we can cancel the while loop
var cancellationToken = new CancellationToken();
// Create a StreamReader from the 'hybridConnectionStream`
var streamReader = new StreamReader(hybridConnectionStream);

while (!cancellationToken.IsCancellationRequested)
{
    // Read a line of input until a newline is encountered
    var line = await streamReader.ReadLineAsync();
    if (string.IsNullOrEmpty(line))
    {
        // If there's no input data, we will signal that 
        // we will no longer send data on this connection
        // and then break out of the processing loop.
        await hybridConnectionStream.ShutdownAsync(cancellationToken);
        break;
    }
}
```

### <a name="sending-data"></a><span data-ttu-id="e895a-125">Verzenden van gegevens</span><span class="sxs-lookup"><span data-stu-id="e895a-125">Sending data</span></span>
<span data-ttu-id="e895a-126">Wanneer u een verbinding tot stand gebracht, kunt u een bericht verzenden naar de Relay-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="e895a-126">Once you have a connection established, you can send a message to the Relay endpoint.</span></span> <span data-ttu-id="e895a-127">Omdat het verbindingsobject neemt over [stroom](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), verzenden van uw gegevens als een `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="e895a-127">Because the connection object inherits [Stream](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), send your data as a `byte[]`.</span></span> <span data-ttu-id="e895a-128">Het volgende voorbeeld ziet u hoe u dit doet:</span><span class="sxs-lookup"><span data-stu-id="e895a-128">The following example shows how to do this:</span></span>

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

<span data-ttu-id="e895a-129">Echter, als u tekst rechtstreeks verzenden wilt zonder de voor het coderen van de tekenreeks telkens wanneer u terugloopt de `hybridConnectionStream` object met een [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) object.</span><span class="sxs-lookup"><span data-stu-id="e895a-129">However, if you want to send text directly, without needing to encode the string each time, you can wrap the `hybridConnectionStream` object with a [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) object.</span></span>

```csharp
// The StreamWriter object only needs to be created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a><span data-ttu-id="e895a-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e895a-130">Next steps</span></span>
<span data-ttu-id="e895a-131">Volg deze koppelingen voor meer informatie over Azure Relay:</span><span class="sxs-lookup"><span data-stu-id="e895a-131">To learn more about Azure Relay, visit these links:</span></span>

* [<span data-ttu-id="e895a-132">Microsoft.Azure.Relay verwijzing</span><span class="sxs-lookup"><span data-stu-id="e895a-132">Microsoft.Azure.Relay reference</span></span>](/dotnet/api/microsoft.azure.relay)
* [<span data-ttu-id="e895a-133">Wat is Azure Relay?</span><span class="sxs-lookup"><span data-stu-id="e895a-133">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="e895a-134">Beschikbare Relay-API 's</span><span class="sxs-lookup"><span data-stu-id="e895a-134">Available Relay APIs</span></span>](relay-api-overview.md)

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener