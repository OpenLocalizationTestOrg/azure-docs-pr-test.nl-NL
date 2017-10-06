---
title: aaaHow toouse Azure Service Bus Hello WebJobs SDK
description: Meer informatie over hoe Hallo toouse Azure Service Bus-wachtrijen en onderwerpen met de WebJobs SDK.
services: app-service\web, service-bus
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 2114a934-135b-42b8-871c-6cc040214e76
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: cb801a9320a20c276da4f48c8941c09d3f09bb1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-service-bus-with-hello-webjobs-sdk"></a><span data-ttu-id="52324-103">Hoe toouse Azure Service Bus met Hallo WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="52324-103">How toouse Azure Service Bus with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="52324-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="52324-104">Overview</span></span>
<span data-ttu-id="52324-105">Deze handleiding bevat C# code voorbeelden die tonen hoe tootrigger een proces wanneer er wordt een Azure Service Bus-bericht ontvangen.</span><span class="sxs-lookup"><span data-stu-id="52324-105">This guide provides C# code samples that show how tootrigger a process when an Azure Service Bus message is received.</span></span> <span data-ttu-id="52324-106">Hallo code voorbeelden gebruik [WebJobs SDK](websites-dotnet-webjobs-sdk.md) versie 1.x.</span><span class="sxs-lookup"><span data-stu-id="52324-106">hello code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="52324-107">Hallo handleiding wordt ervan uitgegaan dat u weet [hoe een webtaak-project in Visual Studio met verbinding toocreate dat punt tooyour storage-account tekenreeksen](websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="52324-107">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md).</span></span>

<span data-ttu-id="52324-108">Hallo codefragmenten functies, alleen weergeven niet code die wordt gemaakt van Hallo Hallo `JobHost` object zoals in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="52324-108">hello code snippets only show functions, not hello code that creates hello `JobHost` object as in this example:</span></span>

```
public class Program
{
   public static void Main()
   {
      JobHostConfiguration config = new JobHostConfiguration();
      config.UseServiceBus();
      JobHost host = new JobHost(config);
      host.RunAndBlock();
   }
}
```

<span data-ttu-id="52324-109">Een [volledige Service Bus-codevoorbeeld](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) in hello azure webjobs-sdk samples opslagplaats op GitHub.com is.</span><span class="sxs-lookup"><span data-stu-id="52324-109">A [complete Service Bus code example](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) is in hello azure-webjobs-sdk-samples repository on GitHub.com.</span></span>

## <span data-ttu-id="52324-110"><a id="prerequisites"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="52324-110"><a id="prerequisites"></a> Prerequisites</span></span>
<span data-ttu-id="52324-111">toowork met Service Bus hebt u tooinstall hello [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet pakket bovendien toohello andere pakketten WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="52324-111">toowork with Service Bus you have tooinstall hello [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet package in addition toohello other WebJobs SDK packages.</span></span> 

<span data-ttu-id="52324-112">U hebt ook tooset hello AzureWebJobsServiceBus verbindingsreeks in toevoeging toohello storage-verbindingsreeksen.</span><span class="sxs-lookup"><span data-stu-id="52324-112">You also have tooset hello AzureWebJobsServiceBus connection string in addition toohello storage connection strings.</span></span>  <span data-ttu-id="52324-113">U kunt dit doen in Hallo `connectionStrings` sectie van Hallo App.config-bestand, zoals wordt weergegeven in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="52324-113">You can do this in hello `connectionStrings` section of hello App.config file, as shown in hello following example:</span></span>

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

<span data-ttu-id="52324-114">Zie voor een voorbeeldproject met Hallo Service Bus-verbindingsinstelling tekenreeks in Hallo App.config-bestand, [Service Bus-voorbeeld](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span><span class="sxs-lookup"><span data-stu-id="52324-114">For a sample project that includes hello Service Bus connection string setting in hello App.config file, see [Service Bus example](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span></span> 

<span data-ttu-id="52324-115">Hallo-verbindingsreeksen kunnen ook worden ingesteld in hello Azure runtime-omgeving, waarmee vervolgens Hallo App.config instellingen overschreven wanneer Hallo webtaak wordt uitgevoerd in Azure. Zie voor meer informatie [aan de slag met de WebJobs SDK Hallo](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span><span class="sxs-lookup"><span data-stu-id="52324-115">hello connection strings can also be set in hello Azure runtime environment, which then overrides hello App.config settings when hello WebJob runs in Azure; for more information, see [Get Started with hello WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span></span>

## <span data-ttu-id="52324-116"><a id="trigger"></a>Hoe tootrigger een functie als een Service Bus-wachtrij bericht wordt ontvangen</span><span class="sxs-lookup"><span data-stu-id="52324-116"><a id="trigger"></a> How tootrigger a function when a Service Bus queue message is received</span></span>
<span data-ttu-id="52324-117">toowrite een functie die Hallo WebJobs SDK wordt aangeroepen wanneer een wachtrijbericht wordt ontvangen, gebruikt u Hallo `ServiceBusTrigger` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="52324-117">toowrite a function that hello WebJobs SDK calls when a queue message is received, use hello `ServiceBusTrigger` attribute.</span></span> <span data-ttu-id="52324-118">Hallo kenmerkconstructor heeft een parameter met de naam Hallo van Hallo wachtrij toopoll.</span><span class="sxs-lookup"><span data-stu-id="52324-118">hello attribute constructor takes a parameter that specifies hello name of hello queue toopoll.</span></span>

### <a name="how-servicebustrigger-works"></a><span data-ttu-id="52324-119">De werking van ServiceBusTrigger</span><span class="sxs-lookup"><span data-stu-id="52324-119">How ServiceBusTrigger works</span></span>
<span data-ttu-id="52324-120">Hallo SDK een bericht ontvangt in `PeekLock` modus en aanroepen `Complete` op het Hallo-bericht als Hallo-functie wordt voltooid of aanroepen `Abandon` als Hallo-functie is mislukt.</span><span class="sxs-lookup"><span data-stu-id="52324-120">hello SDK receives a message in `PeekLock` mode and calls `Complete` on hello message if hello function finishes successfully, or calls `Abandon` if hello function fails.</span></span> <span data-ttu-id="52324-121">Als het Hallo-functie wordt uitgevoerd langer dan Hallo `PeekLock` time-out Hallo vergrendeling automatisch wordt vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="52324-121">If hello function runs longer than hello `PeekLock` timeout, hello lock is automatically renewed.</span></span>

<span data-ttu-id="52324-122">Service Bus omgaat met een eigen verontreinigd wachtrij die niet kunnen worden beheerd of geconfigureerd door Hallo WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="52324-122">Service Bus does its own poison queue handling which cannot be controlled or configured by hello WebJobs SDK.</span></span> 

### <a name="string-queue-message"></a><span data-ttu-id="52324-123">Tekenreeks wachtrijbericht</span><span class="sxs-lookup"><span data-stu-id="52324-123">String queue message</span></span>
<span data-ttu-id="52324-124">Hallo leest codevoorbeeld een wachtrijbericht die een tekenreeks bevat en schrijft Hallo tekenreeks toohello WebJobs SDK-dashboard.</span><span class="sxs-lookup"><span data-stu-id="52324-124">hello following code sample reads a queue message that contains a string and writes hello string toohello WebJobs SDK dashboard.</span></span>

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

<span data-ttu-id="52324-125">**Opmerking:** als u Hallo berichten in wachtrij plaatsen in een toepassing die geen gebruik maakt van Hallo WebJobs SDK maakt, moet u ervoor tooset [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) te "text/plain'.</span><span class="sxs-lookup"><span data-stu-id="52324-125">**Note:** If you are creating hello queue messages in an application that doesn't use hello WebJobs SDK, make sure tooset [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) too"text/plain".</span></span>

### <a name="poco-queue-message"></a><span data-ttu-id="52324-126">POCO wachtrijbericht</span><span class="sxs-lookup"><span data-stu-id="52324-126">POCO queue message</span></span>
<span data-ttu-id="52324-127">Hallo SDK wordt automatisch een wachtrijbericht met JSON voor een POCO deserialiseren [(Plain oude CLR-Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) type.</span><span class="sxs-lookup"><span data-stu-id="52324-127">hello SDK will automatically deserialize a queue message that contains JSON for a POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) type.</span></span> <span data-ttu-id="52324-128">Hallo codevoorbeeld leest het bericht van een wachtrij met een `BlobInformation` object waarvoor een `BlobName` eigenschap:</span><span class="sxs-lookup"><span data-stu-id="52324-128">hello following code sample reads a queue message that contains a `BlobInformation` object which has a `BlobName` property:</span></span>

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

<span data-ttu-id="52324-129">Codevoorbeelden die laat zien hoe toouse eigenschappen van Hallo POCO toowork met blobs en tabellen in dezelfde Hallo werkt, kunt u Hallo [opslag wachtrijen versie van dit artikel](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span><span class="sxs-lookup"><span data-stu-id="52324-129">For code samples showing how toouse properties of hello POCO toowork with blobs and tables in hello same function, see hello [storage queues version of this article](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span></span>

<span data-ttu-id="52324-130">Als uw code die wachtrij het Hallo-bericht maakt geen gebruik maakt van Hallo WebJobs SDK, gebruikt u code vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="52324-130">If your code that creates hello queue message doesn't use hello WebJobs SDK, use code similar toohello following example:</span></span>

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a><span data-ttu-id="52324-131">Typen ServiceBusTrigger werkt met</span><span class="sxs-lookup"><span data-stu-id="52324-131">Types ServiceBusTrigger works with</span></span>
<span data-ttu-id="52324-132">Naast `string` en POCO-typen, kunt u Hallo `ServiceBusTrigger` kenmerk met een bytematrix of een `BrokeredMessage` object.</span><span class="sxs-lookup"><span data-stu-id="52324-132">Besides `string` and POCO  types, you can use hello `ServiceBusTrigger` attribute with a byte array or a `BrokeredMessage` object.</span></span>

## <span data-ttu-id="52324-133"><a id="create"></a>Hoe wachtrij toocreate Service Bus-berichten</span><span class="sxs-lookup"><span data-stu-id="52324-133"><a id="create"></a> How toocreate Service Bus queue messages</span></span>
<span data-ttu-id="52324-134">toowrite een functie die een nieuwe wachtrijbericht maakt gebruik van Hallo `ServiceBus` kenmerk en Hallo wachtrij naam toohello kenmerkconstructor doorgeven.</span><span class="sxs-lookup"><span data-stu-id="52324-134">toowrite a function that creates a new queue message use hello `ServiceBus` attribute and pass in hello queue name toohello attribute constructor.</span></span> 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a><span data-ttu-id="52324-135">Een enkel wachtrijbericht in een niet-async-functie maken</span><span class="sxs-lookup"><span data-stu-id="52324-135">Create a single queue message in a non-async function</span></span>
<span data-ttu-id="52324-136">Hallo volgende codevoorbeeld maakt gebruik van een output-parameter toocreate een nieuw bericht in de wachtrij Hallo met de naam 'outputqueue' Hello dezelfde inhoud als bericht ontvangen in Hallo wachtrij met de naam 'inputqueue' Hallo.</span><span class="sxs-lookup"><span data-stu-id="52324-136">hello following code sample uses an output parameter toocreate a new message in hello queue named "outputqueue" with hello same content as hello message received in hello queue named "inputqueue".</span></span>

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

<span data-ttu-id="52324-137">Hallo output-parameter voor het maken van een enkel wachtrijbericht mag geen van de volgende typen Hallo:</span><span class="sxs-lookup"><span data-stu-id="52324-137">hello output parameter for creating a single queue message can be any of hello following types:</span></span>

* `string`
* `byte[]`
* `BrokeredMessage`
* <span data-ttu-id="52324-138">Een serialiseerbare POCO-type dat u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="52324-138">A serializable POCO type that you define.</span></span> <span data-ttu-id="52324-139">Automatisch geserialiseerd als JSON.</span><span class="sxs-lookup"><span data-stu-id="52324-139">Automatically serialized as JSON.</span></span>

<span data-ttu-id="52324-140">Voor de parameters van het type POCO, een wachtrijbericht altijd gemaakt wanneer het Hallo-functie wordt beëindigd. Als Hallo parameter null is, maakt het Hallo SDK een wachtrijbericht dat null wordt geretourneerd wanneer het Hallo-bericht is ontvangen en gedeserialiseerd.</span><span class="sxs-lookup"><span data-stu-id="52324-140">For POCO type parameters, a queue message is always created when hello function ends; if hello parameter is null, hello SDK creates a queue message that will return null when hello message is received and deserialized.</span></span> <span data-ttu-id="52324-141">Hallo voor andere typen, als Hallo parameter null is geen wachtrijbericht is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="52324-141">For hello other types, if hello parameter is null no queue message is created.</span></span>

### <a name="create-multiple-queue-messages-or-in-async-functions"></a><span data-ttu-id="52324-142">Maken van meerdere berichten in wachtrij plaatsen of in een async-functies</span><span class="sxs-lookup"><span data-stu-id="52324-142">Create multiple queue messages or in async functions</span></span>
<span data-ttu-id="52324-143">toocreate meerdere berichten gebruiken Hallo `ServiceBus` met kenmerk `ICollector<T>` of `IAsyncCollector<T>`, zoals weergegeven in het volgende codevoorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="52324-143">toocreate multiple messages, use  hello `ServiceBus` attribute with `ICollector<T>` or `IAsyncCollector<T>`, as shown in hello following code sample:</span></span>

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="52324-144">Het bericht voor elke wachtrij wordt gemaakt bij direct hello `Add` methode wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="52324-144">Each queue message is created immediately when hello `Add` method is called.</span></span>

## <span data-ttu-id="52324-145"><a id="topics"></a>Hoe toowork met Service Bus-onderwerpen</span><span class="sxs-lookup"><span data-stu-id="52324-145"><a id="topics"></a>How toowork with Service Bus topics</span></span>
<span data-ttu-id="52324-146">toowrite een functie die Hallo SDK-aanroepen wanneer een bericht wordt ontvangen op een Service Bus-onderwerp, gebruikt u Hallo `ServiceBusTrigger` kenmerk met de Hallo-constructor die onderwerpnaam en de naam van het abonnement, zoals wordt weergegeven in het volgende codevoorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="52324-146">toowrite a function that hello SDK calls when a message is received on a Service Bus topic, use hello `ServiceBusTrigger` attribute with hello constructor that takes topic name and subscription name, as shown in hello following code sample:</span></span>

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

<span data-ttu-id="52324-147">een bericht op een onderwerp, gebruik Hallo toocreate `ServiceBus` kenmerk met een onderwerp naam Hallo dezelfde manier gebruiken met de naam van een wachtrij.</span><span class="sxs-lookup"><span data-stu-id="52324-147">toocreate a message on a topic, use hello `ServiceBus` attribute with a topic name hello same way you use it with a queue name.</span></span>

## <a name="features-added-in-release-11"></a><span data-ttu-id="52324-148">Functies die zijn toegevoegd in versie 1.1</span><span class="sxs-lookup"><span data-stu-id="52324-148">Features added in release 1.1</span></span>
<span data-ttu-id="52324-149">Hallo volgende kenmerken zijn toegevoegd in versie 1.1:</span><span class="sxs-lookup"><span data-stu-id="52324-149">hello following features were added in release 1.1:</span></span>

* <span data-ttu-id="52324-150">Toestaan grondige aanpassing van de berichtverwerking `ServiceBusConfiguration.MessagingProvider`.</span><span class="sxs-lookup"><span data-stu-id="52324-150">Allow deep customization of message processing via `ServiceBusConfiguration.MessagingProvider`.</span></span>
* <span data-ttu-id="52324-151">`MessagingProvider`biedt ondersteuning voor aanpassing van Service Bus Hallo `MessagingFactory` en `NamespaceManager`.</span><span class="sxs-lookup"><span data-stu-id="52324-151">`MessagingProvider` supports customization of hello Service Bus `MessagingFactory` and `NamespaceManager`.</span></span>
* <span data-ttu-id="52324-152">Een `MessageProcessor` strategiepatroon kunt u toospecify een processor per wachtrij/onderwerp.</span><span class="sxs-lookup"><span data-stu-id="52324-152">A `MessageProcessor` strategy pattern allows you toospecify a processor per queue/topic.</span></span>
* <span data-ttu-id="52324-153">Verwerking gelijktijdigheid van bericht is standaard ondersteund.</span><span class="sxs-lookup"><span data-stu-id="52324-153">Message processing concurrency is supported by default.</span></span> 
* <span data-ttu-id="52324-154">Eenvoudige aanpassing van `OnMessageOptions` via `ServiceBusConfiguration.MessageOptions`.</span><span class="sxs-lookup"><span data-stu-id="52324-154">Easy customization of `OnMessageOptions` via `ServiceBusConfiguration.MessageOptions`.</span></span>
* <span data-ttu-id="52324-155">Toestaan dat [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) toobe opgegeven op `ServiceBusTriggerAttribute` / `ServiceBusAttribute` (voor scenario's waarbij u mogelijk geen rechten beheren).</span><span class="sxs-lookup"><span data-stu-id="52324-155">Allow [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) toobe specified on `ServiceBusTriggerAttribute`/`ServiceBusAttribute` (for scenarios where you might not have Manage rights).</span></span> <span data-ttu-id="52324-156">Houd er rekening mee dat Azure WebJobs niet kan tooautomatically inrichten niet-bestaande wachtrijen en onderwerpen zonder AccessRights beheren.</span><span class="sxs-lookup"><span data-stu-id="52324-156">Note that Azure WebJobs is unable tooautomatically provision non-existent queues and topics without Manage AccessRights.</span></span>

## <span data-ttu-id="52324-157"><a id="queues"></a>Verwante onderwerpen Hallo opslag wachtrijen hoe tooarticle vallen</span><span class="sxs-lookup"><span data-stu-id="52324-157"><a id="queues"></a>Related topics covered by hello storage queues how-tooarticle</span></span>
<span data-ttu-id="52324-158">Zie voor informatie over WebJobs SDK scenario's niet specifiek tooService Bus, [hoe toouse Azure queue storage Hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="52324-158">For information about WebJobs SDK scenarios not specific tooService Bus, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="52324-159">Onderwerpen in dit artikel zijn Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="52324-159">Topics covered in that article include hello following:</span></span>

* <span data-ttu-id="52324-160">Async-functies</span><span class="sxs-lookup"><span data-stu-id="52324-160">Async functions</span></span>
* <span data-ttu-id="52324-161">Meerdere exemplaren</span><span class="sxs-lookup"><span data-stu-id="52324-161">Multiple instances</span></span>
* <span data-ttu-id="52324-162">Correct afsluiten</span><span class="sxs-lookup"><span data-stu-id="52324-162">Graceful shutdown</span></span>
* <span data-ttu-id="52324-163">Kenmerken in de hoofdtekst van een functie Hallo WebJobs SDK gebruiken</span><span class="sxs-lookup"><span data-stu-id="52324-163">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="52324-164">Hallo SDK verbindingsreeksen instellen in code</span><span class="sxs-lookup"><span data-stu-id="52324-164">Set hello SDK connection strings in code</span></span>
* <span data-ttu-id="52324-165">Waarden instellen voor de WebJobs SDK constructorparameters in code</span><span class="sxs-lookup"><span data-stu-id="52324-165">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="52324-166">Een functie handmatig activeren</span><span class="sxs-lookup"><span data-stu-id="52324-166">Trigger a function manually</span></span>
* <span data-ttu-id="52324-167">Schrijven Logboeken</span><span class="sxs-lookup"><span data-stu-id="52324-167">Write logs</span></span>

## <span data-ttu-id="52324-168"><a id="nextsteps"></a> Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="52324-168"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="52324-169">Deze handleiding hebt gekregen code voorbeelden die tonen hoe toohandle algemene scenario's voor het werken met Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="52324-169">This guide has provided code samples that show how toohandle common scenarios for working with Azure Service Bus.</span></span> <span data-ttu-id="52324-170">Voor meer informatie over hoe toouse Azure WebJobs en Hallo WebJobs SDK zien [Azure WebJobs aanbevolen Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="52324-170">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

